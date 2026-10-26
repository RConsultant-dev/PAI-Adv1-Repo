# PAI-Adv1-Repo
PAI-Adv1-Repo (PAI応用1_最終課題)

## 概要
### フォルダ構成
・navigation  
実行時に取得したnoitagivanナビゲーションファイル（my_map.pgm, my_map.yaml）
およびros2bagの集計情報（ros2bag_info.txt）

・bot_prototype  
draftの.sdfや.yaml、.rvizなどがある（評価段階で使用したもので、タスク実行では使用しない）

### 使用環境
(1) 基本構成  
Ubuntu 22.04 Jammy, 
ROS 2 Humble, 
Gazebo Fortress, 
Docker 29.7.2, 
Windows11+WSL

(2) ROS2パッケージ  
Turtlebot3, 
turtlebot3_gazebo, 
turtlebot3_navigation2, 
turtlebot3_teleop, 
Gazebo+RViz2, 
nav2_map_server, 
ros2bag

### タスク実行の準備
1. マップの作製
- Gazeboシミュレータの実行  
$ ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py  
- navigation2の起動  
$ ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True slam:=True  
- turtlebot3のコントロール  
$ ros2 run turtlebot3_teleop teleop_keyboard  
- テレオペでマップを作製する  
$ ros2 run nav2_map_server map_saver_cli -f navigation/my_map  

2. マップのシミュレータ活用と移動経路決定
- Gazeboシミュレータの実行  
$ ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py  
- navigation2を起動し、作成したマップをRViz2に反映する  
$ ros2 launch turtlebot3_navigation2 navigation2.launch.py use_sim_time:=True map:=navigation/my_map.yaml  

- ゴール設定とコースを設定する  
結果はros2bagで記録する  
$ ros2 bag record -a -o rosbag2_2026_10_25-10_32_50  
- ros2bagのデータはサイズが大きいため、ここではその情報のみ収集して掲載する。  
$ ros2 bag info rosbag2_2026_10_25-10_32_50 > navigation/ros2bag_info.txt  

### タスクの実行
- Gazeboシミュレータの実行  
$ ros2 launch turtlebot3_gazebo turtlebot3_house.launch.py  
- turtlebot3のコントロール  
- ros2bagで記録したメッセージを再生する  
$ ros2 bag play -o rosbag2_2026_10_25-10_32_50  

=====
