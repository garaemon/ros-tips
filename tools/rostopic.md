rostopic
===

概要
---
topicについての情報を調べるツール。

### 特定のtopicに対してpublish/subscribeしているノードを調べる
* [rosnode info](rosnode.md#特定のノードが何をpub/subしているか調べる)と組み合わせてデバッグしていく。
* 特にトピック-ノードによって作られるネットワークが何処かで切れてしまっている場合に有効.
 * `rostopic info` -> `rosnode info` -> `rostopic info` -> ...とやって何処で問題があるのかを順に探っていく
* システムがうまく動いていないときにまずこれをやってみると良い。
```sh
$ rostopic info /initialpose
Type: geometry_msgs/PoseWithCovarianceStamped

Publishers:
 * /rviz_for_interactive_marker (http://10.68.0.136:60895/)
 * /initialpose3d (http://pr1012:47315/)
 * /move_base_db (http://pr1012:46427/)
 * /jsk_startup_rviz (http://133.11.216.33:44831/)

Subscribers:
* /amcl (http://pr1012s:38949/)
$ rosnode info /move_base_db
Node [/move_base_db]
Publications:
 * /rosout [rosgraph_msgs/Log]
 * /tf2_buffer_server/goal [tf2_msgs/LookupTransformActionGoal]
 * /tf2_buffer_server/cancel [actionlib_msgs/GoalID]
 * /initialpose [geometry_msgs/PoseWithCovarianceStamped]

Subscriptions:
 * /tf2_buffer_server/feedback [tf2_msgs/LookupTransformActionFeedback]
 * /tf2_buffer_server/result [tf2_msgs/LookupTransformActionResult]
 * /tf2_buffer_server/status [actionlib_msgs/GoalStatusArray]
...
 ```
