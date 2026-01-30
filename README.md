# x-humanoid training toolchain

**[简体中文](./README_zh.md)｜English**

## Project Introduction

This project provides a training toolchain for adapting Walker TienKung humanoid robots with the open-source LeRobot framework. It enables users to train embodied manipulation models for Walker TienKung robots based on the Lerobot.

## Project Structure

```
x-humanoid-training-toolchain/
├── lerobot/                 # Core library
│   ├── common/              # Common utilities
│   ├── configs/             # Configuration files
│   ├── scripts/             # Training & evaluation scripts
│   └── templates/           # Template files
├── scripts/                 # Data conversion scripts
│   ├── configs/             # Conversion configs
│   ├── convert.sh           # Conversion shell script
│   └── convert_to_lerobot.py
├── deployment/              # Deployment code
│   ├── action_policy.py     # Action policy
│   └── ros2_deployment_*.py # ROS2 deployment
├── examples/                # Example code & tutorials
├── benchmarks/              # Benchmarks
├── tests/                   # Test code
├── docker/                  # Docker configuration
├── train_example/           # Training examples
└── static/                  # Static resources
```

## Usage Instructions

This step converts HDF5-formatted data into the LeRobotDataset format by parsing structured observations (RGB images, joints, etc.).

```
cd scripts
sh convert.sh #Modify the path and args. 
```

```
--config
Description: Path to the configuration JSON file containing settings for the application.
--repo_id
Description: ID for the dataset.
--src_root
Description: Source directory containing raw input data files.
--tgt_path
Description: Target directory path for processed output files.
--task_name
Description: Identifier for the current processing task.
--fps
Description: Frames per second setting for video processing operations.
--robot_type
Description: Identifier for robot hardware platform.
```



## Training

After converting the dataset to LeRobotDataset format, users can train models using the following workflow:

- Configuration setup
  Create a train_config.json file to specify the dataset path, training algorithm (e.g., ACT or Diffusion Policy), hyperparameters (learning rate, batch size), and other relevant parameters.
- Training process
  With the configuration file prepared, initiate training by running the command:

```
export HF_LEROBOT_HOME=PATH_TO_LEROBOT_HOME
python lerobot/scripts/train.py --config_path=PATH_TO_CONFIG
```



## Visualization

Dataset visualization is performed using LeRobot's built-in visualization scripts.

```
python lerobot/scripts/visualize_dataset.py --repo-id ID --episode-index 0 --root PATH_TO_ROOT
```

## Acknowledgement

**Special thanks to the Beijing Humanoid Robot Innovation Center for their invaluable support and guidance.**

**Project Link:** [x-humanoid-training-toolchain](https://github.com/Open-X-Humanoid/x-humanoid-training-toolchain)
