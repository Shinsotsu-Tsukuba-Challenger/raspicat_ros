# raspicat_ros

## Build Status

## Requirements

- Raspberry Pi Cat
  - https://rt-net.jp/products/raspberry-pi-cat/
- Linux OS
  - [Ubuntu Server 22.04](https://ubuntu.com/download/raspberry-pi)
- Device Driver
  - [rt-net/RaspberryPiMouse](https://github.com/rt-net/RaspberryPiMouse)
- ROS 2
  - [Humble Hawksbill](https://docs.ros.org/en/humble/Installation.html)

ROS 2とLinux OSは以下の組み合わせでのみ確認しています

* ROS 2 Humble + Ubuntu 22.04

## Installation

### Source Build

```sh
# パッケージのダウンロード
cd ~/catkin_ws/src
git clone -b $ROS_DISTRO-devel https://github.com/rt-net/raspimouse2.git
git clone -b ros2 https://github.com/rt-net/raspicat_ros.git
git clone -b ros2 https://github.com/rt-net/raspicat_description.git

# 依存パッケージのインストール
rosdep update
rosdep install -r -y -i --from-paths raspicat* raspimouse*

# ビルド＆インストール
cd ~/catkin_ws
colcon build --symlink-install
source ~/catkin_ws/install/setup.bash
```

## QuickStart

```sh
# 端末 1
source ~/catkin_ws/install/setup.bash
ros2 launch raspicat_bringup raspicat.launch.py

# 端末 2
# モータの回転
source ~/catkin_ws/install/setup.bash
ros2 service call /motor_power std_srvs/SetBool '{data: true}'
ros2 topic pub -1 /cmd_vel geometry_msgs/Twist '{linear: {x: 0.15, y: 0, z: 0}, angular: {x: 0, y: 0, z: 0.1}}'
```

## License

(C) 2018-2023 RT Corporation

各ファイルはライセンスがファイル中に明記されている場合、そのライセンスに従います。特に明記されていない場合は、Apache License, Version 2.0に基づき公開されています。  
ライセンスの全文は[LICENSE](./LICENSE)または[https://www.apache.org/licenses/LICENSE-2.0](https://www.apache.org/licenses/LICENSE-2.0)から確認できます。

※このソフトウェアは基本的にオープンソースソフトウェアとして「AS IS」（現状有姿のまま）で提供しています。本ソフトウェアに関する無償サポートはありません。  
バグの修正や誤字脱字の修正に関するリクエストは常に受け付けていますが、それ以外の機能追加等のリクエストについては社内のガイドラインを優先します。