# Static Transform Mux

This ROS node subscribes to `/tf_static`, collects all the transforms that are ever published there, and re-sends a
message that contains not only the transforms from the last publisher, but all transforms ever encountered.

This is a workaround for e.g. [geometry2#181](https://github.com/ros/geometry2/issues/181), or for anybody else who
needs to have multiple static transform publishers in the system.

## Node `static\_transform\_mux`

### Subscribed topics

* `/tf_static`: The static transforms.

### Published topics 

* `/tf_static` (`tf2_msgs/TFMessage` latched): Again, the static transforms. Special care is taken so that this node 
does not react to its own messages.
* `ready` (`std_msgs/Bool` latched): This message is sent (and latched) once the first message on `/tf_static` is 
published by this node, so that other nodes that rely on this node's operation know that it has been brought up.

### Parameters

* `~update_only_with_newer` (`bool`, defaults to `False`): If set to True, only transforms with newer timestamps can 
substitute an already cached transform (otherwise, the latest received tranform is used.)
* `~forbidden_callerid_prefix` (`str` or `None`, defaults to `None`): This parameter can contain a prefix of 
[`callerid`s](http://wiki.ros.org/ROS/Master_API) that will additionally be ignored by the `/tf_static` callback.
Using this parameter is required if you transmit `/tf_static` over some non-ROS connection which changes or
discards the `callerid` (e.g. when using [`nimbro_network`](https://github.com/AIS-Bonn/nimbro_network/)). 