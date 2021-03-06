roslaunch
===

概要
---
多くのROSのノード(プロセス)をひとつずつ立ち上げるのは面倒なので、xmlファイルにまとめて書いて
一気に立ち上げられるようにするためのツール。

### ノード一覧の取得
```sh
$ roslaunch openni2_launch openni2.launch --nodes
/camera/camera_nodelet_manager
/camera/driver
/camera/rectify_color
/camera/depth_rectify_depth
/camera/depth_metric_rect
/camera/depth_metric
/camera/depth_points
/camera/register_depth_rgb
/camera/points_xyzrgb_sw_registered
/camera_base_link
/camera_base_link1
/camera_base_link2
/camera_base_link3
```

* grepと組み合わせて
```sh
$ roslaunch openni2_launch openni2.launch --nodes | grep driver
/camera/driver
```

### ノード立ち上げの引数を取得する
```sh
$ roslaunch hoge_pkg fuga.launch --args piyo_node
```

* grepと`--nodes`と組み合わせて使う
  * 引数のチェック
  * 障害時に一つのノードのみ立ち上げる
  * 一つだけgdbで上げてデバッグする
```sh
$ roslaunch openni2_launch openni2.launch --nodes | grep driver
/camera/driver
$ roslaunch openni2_launch openni2.launch --args /camera/driver
ROS_NAMESPACE=/camera /opt/ros/hydro/lib/nodelet/nodelet load openni2_camera/OpenNI2DriverNodelet camera_nodelet_manager ir:=ir rgb:=rgb depth:=depth depth_registered:=depth_registered rgb/image:=rgb/image_raw depth/image:=depth_registered/image_raw __name:=driver
$ roslaunch openni2_launch openni2.launch --args /camera/driver | bash
$ gdb --args $(roslaunch openni2_launch openni2.launch --args /camera/driver)
```

### gdbつきで立ち上げる
* ターミナルを分離するためにxterm越しに立ち上げる
* `launch-prefix`をnodeタグに追加する
```xml
<node pkg="foo" type="bar" name="foobar"
      launch-prefix="xterm -e gdb --args">
...
</node>
```
