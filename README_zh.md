# x-humanoid training toolchain

**[English](./README.md)｜简体中文**

## 项目介绍

本项目是天工行者机器人对于 Lerobot 开源框架适配的训练工具链。使用此项目，用户可以基于 Lerobot 开源框架的算法实现天工行者机器人的具身操作。

## 项目架构

```
x-humanoid-training-toolchain/
├── lerobot/                 # 核心库
│   ├── common/              # 通用工具
│   ├── configs/             # 配置文件
│   ├── scripts/             # 训练和评估脚本
│   └── templates/           # 模板文件
├── scripts/                 # 数据转换脚本
│   ├── configs/             # 转换配置
│   ├── convert.sh           # 转换脚本
│   └── convert_to_lerobot.py
├── deployment/              # 部署代码
│   ├── action_policy.py     # 动作策略
│   └── ros2_deployment_*.py # ROS2部署
├── examples/                # 示例代码和教程
├── benchmarks/              # 基准测试
├── tests/                   # 测试代码
├── docker/                  # Docker配置
├── train_example/           # 训练示例
└── static/                  # 静态资源
```

## 使用说明

读取 hdf5 格式的数据，根据定义的 keys 解析 observations（images, joints, etc.）。

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



## 模型训练

将数据集转换为 LeRobot 的格式后，用户可以使用以下工作流程进行模型训练：

- 训练配置。
  创建一个 train_config. json 文件来指定数据集路径、训练算法（例如，ACT或扩散策略）、超参数（学习率、批大小）和其他相关参数。
- 创建配置文件后，用户可以通过执行以下命令开始模型训练：

```
export HF_LEROBOT_HOME=PATH_TO_LEROBOT_HOME
python lerobot/scripts/train.py --config_path=PATH_TO_CONFIG

```



## 可视化

使用 LeRobot 的本地工具进行数据集的可视化。

```
python lerobot/scripts/visualize_dataset.py --repo-id ID --episode-index 0 --root PATH_TO_ROOT
```



##  致谢

**特别感谢北京人形机器人创新中心提供的宝贵支持与指导。**

**项目链接：** [x-humanoid-training-toolchain](https://github.com/Open-X-Humanoid/x-humanoid-training-toolchain)
