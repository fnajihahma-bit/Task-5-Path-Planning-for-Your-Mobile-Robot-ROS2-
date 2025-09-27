# Task-5-Path-Planning-for-Your-Mobile-Robot-ROS2-
Simulation


## 🙋 Submitted By

- **Name:** Fatin Najihah Binti Mat Ali  
- **Student ID:** 2024853488
---

## 🛠 Requirements

- Ubuntu **22.04 LTS**
- ROS2 **Humble**
- `turtlebot3_navigation2` & `nav2_bringup` packages
- TurtleBot3 or **custom URDF model** (from Task 4)
- Map from Task 3: `sim_map.yaml` & `sim_map.pgm`
- RViz2 for visualization
- Gazebo simulator

### 📁 Repository Structure

```markdown
/week5_task_ros2/
├── README.md                  # This file
├── img/
│   ├── nav2_goal.png
│   ├── nav2_path.png
│   └── custom_robot_path.png
├── video/
│   └── path_planning_demo.mp4
└── reflection.pdf             # Written reflection (200–300 words)
```

## 🧪 Step-by-Step Instructions

### 1️⃣ Launch TurtleBot3 Simulation

```bash
export TURTLEBOT3_MODEL=burger
ros2 launch turtlebot3_gazebo turtlebot3_world.launch.py
```

### 2️⃣ Launch Navigation2 with Saved Map

```bash
ros2 launch turtlebot3_navigation2 navigation2.launch.py \
use_sim_time:=True map:=$HOME/sim_map.yaml
```

### 3️⃣ Use RViz2 for Navigation

- Click "2D Pose Estimate" to set the robot’s start location.
- Click "Nav2 Goal" to send a destination.
- The robot should now autonomously plan and follow the path while avoiding obstacles.

### 🤖 4️⃣ Apply to Your Custom Robot

- Replace the TurtleBot3 URDF with custom robot model (from Task 4).

- Ensure your robot has:
  - Valid sensor plugins (e.g., LIDAR or depth camera).
  - Correct TF tree and URDF configuration.

- Launch Nav2 using your custom launch file with:
  - Robot description
  - Map
  - Navigation parameters

### 🔧 Adjusting Path Behavior — TurtleBot3 Inflation Parameters

To tune how closely the robot can pass near obstacles, you can adjust the inflation layer in burger.yaml.

📍 Example:
# File: burger.yaml

```yaml
local_costmap:
  local_costmap:
    ros__parameters:
      ...
      inflation_layer:
        plugin: "nav2_costmap_2d::InflationLayer"
        inflation_radius: 0.15        # ⬅️ Reduce from 0.55 for tighter paths
        cost_scaling_factor: 5.0      # ⬅️ Increase to sharpen cost decay

global_costmap:
  global_costmap:
    ros__parameters:
      ...
      inflation_layer:
        plugin: "nav2_costmap_2d::InflationLayer"
        inflation_radius: 0.15
        cost_scaling_factor: 5.0
```
