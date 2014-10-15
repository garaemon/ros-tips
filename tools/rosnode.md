rosnode
===

概要
---
ノードの情報を調べる.

### 特定のノードが何をpub/subしているか調べる
* subscribeしているけどpublishしている相手がいないとき、型情報がunknownになる.
  * 下の例だと`/tf_static`

```sh
$ rosnode info amcl
--------------------------------------------------------------------------------
Node [/amcl]
Publications:
 * /tf [tf2_msgs/TFMessage]
 * /rosout [rosgraph_msgs/Log]
 * /amcl/parameter_updates [dynamic_reconfigure/Config]
 * /particlecloud [geometry_msgs/PoseArray]
 * /amcl_pose [geometry_msgs/PoseWithCovarianceStamped]
 * /amcl/parameter_descriptions [dynamic_reconfigure/ConfigDescription]

Subscriptions:
 * /tf_static [unknown type]
 * /tf [tf2_msgs/TFMessage]
 * /base_scan [sensor_msgs/LaserScan]
 * /initialpose [geometry_msgs/PoseWithCovarianceStamped]
 * /map [nav_msgs/OccupancyGrid]

Services:
 * /request_nomotion_update
 * /amcl/set_logger_level
 * /amcl/get_loggers
 * /amcl/set_parameters
 * /global_localization
...
```

### 特定のノードを殺す
* launchファイルで`respawn="true"`で立ち上げられてると自動復活してしまうので注意.
```sh
$ rosnode kill /amcl
```
