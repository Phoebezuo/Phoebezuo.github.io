---
layout:     post
title:      Unitree SDK2 Setup for Go2 and G1
date:       2026-05-31
summary:    Step by step notes for using unitree_sdk2 to connect with Unitree Go2 or G1 robots
categories: Robotics Unitree SDK
---

This note explains how to use [`unitree_sdk2`](https://github.com/unitreerobotics/unitree_sdk2) to connect a computer with a Unitree Go2 or G1 robot.

## Step 1: Prepare the computer

The official prebuilt environment is:

- Ubuntu 20.04 LTS
- `x86_64` or `aarch64` CPU
- GCC 9.4.0
- CMake 3.10 or newer
- Make

Install the required packages:

```bash
sudo apt-get update
sudo apt-get install -y cmake g++ build-essential libyaml-cpp-dev libeigen3-dev libboost-all-dev libspdlog-dev libfmt-dev
```

## Step 2: Clone the SDK

```bash
git clone https://github.com/unitreerobotics/unitree_sdk2.git
cd unitree_sdk2
```

## Step 3: Build the examples

Build everything from the SDK root:

```bash
mkdir build
cd build
cmake ..
make
```

After this, the example programs are built inside the `build` directory.

## Step 4: Test DDS locally first

Before sending commands to a robot, test that the SDK can run a simple DDS publish/subscribe example.

Open one terminal:

```bash
cd unitree_sdk2/build
./bin/test_publisher
```

Open another terminal:

```bash
cd unitree_sdk2/build
./bin/test_subscriber
```

If the subscriber prints messages from the publisher, the basic SDK communication layer is working.

## Step 5: Connect to the robot network

Connect your computer to the robot by Ethernet or by the network mode recommended for your robot.

Then find the computer's network interface name:

```bash
ip addr
```

Look for the interface that is connected to the robot. Common names look like:

```text
enp2s0
enp3s0
enx00e04c680001
eth0
```

In the commands below, replace `<network_interface>` with your real interface name.

`ip addr` only shows the current network status. It does not change anything. You can run the SDK example directly only if the robot-connected interface already has an IP address in the Unitree robot network.

For example, this is good:

```text
inet 192.168.123.222/24
```

If your interface already shows `192.168.123.xxx/24`, you can skip the manual IP configuration and run the robot example directly.

If your interface has no `inet` address, or it shows a different network such as `192.168.1.xxx`, `10.xxx.xxx.xxx`, or `172.xxx.xxx.xxx`, configure it manually:

```bash
sudo ip addr flush dev <network_interface>
sudo ip addr add 192.168.123.222/24 dev <network_interface>
sudo ip link set <network_interface> up
```

These commands mean:

1. remove the old IP address from this network interface
2. set your computer's IP to `192.168.123.222`
3. turn the network interface on

Be careful with `flush`: it removes the current IP settings on that interface. Use it only on the interface connected to the robot.

## Step 6: Connect with Go2

For Go2, start with the high-level sport client. It is safer than jumping straight into low-level motor control.

From the build directory:

```bash
./bin/go2_sport_client <network_interface>
```

The Go2 sport client example uses `unitree::robot::go2::SportClient`. In the SDK example, common actions include:

- `StandUp()`
- `StandDown()`
- `BalanceStand()`
- `Move(vx, vy, vyaw)`
- `StopMove()`
- `RecoveryStand()`

The example source sets a `TEST_MODE` value. To change the action, edit:

```cpp
const int TEST_MODE = stand_down;
```

For example, to test standing balance, change it to:

```cpp
const int TEST_MODE = balance_stand;
```

Then rebuild:

```bash
make
./bin/go2_sport_client <network_interface>
```

Important: use small movement values first. For example, `Move(0.3, 0, 0.3)` means forward velocity, side velocity, and yaw velocity. Do not test this on a desk or near people.

## Step 7: Connect with G1

For G1, start with the high-level loco client example:

```bash
./bin/g1_loco_client --network_interface=<network_interface> --get_fsm_id
```

Example:

```bash
./bin/g1_loco_client --network_interface=enp2s0 --get_fsm_id
```

If that works, query a few more states:

```bash
./bin/g1_loco_client --network_interface=enp2s0 --get_fsm_mode
./bin/g1_loco_client --network_interface=enp2s0 --get_balance_mode
./bin/g1_loco_client --network_interface=enp2s0 --get_stand_height
```

Then try a simple high-level command:

```bash
./bin/g1_loco_client --network_interface=enp2s0 --balance_stand
```

For controlled movement, the G1 example accepts velocity commands:

```bash
./bin/g1_loco_client --network_interface=enp2s0 --set_velocity="0.1 0 0 1"
```

The four values mean:

1. forward velocity
2. side velocity
3. yaw velocity
4. duration in seconds

Start very small. A humanoid robot can fall, so make sure the robot is in a safe test space and follow Unitree's safety instructions.

## Step 8: Know which example to use

The SDK has different examples for different control levels.

For Go2:

- `go2_sport_client`: high-level movement commands
- `go2_robot_state_client`: robot state query
- `go2_video_client`: video client
- `go2_low_level`: low-level control
- `go2_stand_example`: low-level stand example

For G1:

- `g1_loco_client`: high-level locomotion commands
- `g1_arm5_sdk_dds_example`: arm control for 5-DoF arm
- `g1_arm7_sdk_dds_example`: arm control for 7-DoF arm
- `g1_userctrl_dds_example`: user control through DDS
- `g1_ankle_swing_example`: low-level ankle example
- `g1_audio_client_example`: audio client
- `g1_hand_sdk_example`: hand SDK example

For first connection tests, use high-level examples first:

- Go2: `go2_sport_client`
- G1: `g1_loco_client`

Use low-level examples only after you understand the robot state, control frequency, joint order, and safety behavior.

## Step 9: Install the SDK for your own C++ project

If you want to write your own project instead of only running examples, install the SDK:

```bash
cd unitree_sdk2
mkdir build
cd build
cmake ..
sudo make install
```

Or install it to a custom path:

```bash
cmake .. -DCMAKE_INSTALL_PREFIX=/opt/unitree_robotics
sudo make install
```

If you install it somewhere other than `/opt/unitree_robotics`, make sure CMake can find it through `CMAKE_PREFIX_PATH`.

## Step 10: Basic troubleshooting

If the example cannot connect:

1. Check the network interface name again with `ip addr`.
2. Make sure the computer and robot are on the same network.
3. Make sure you passed the network interface name to the example.
4. Try a state query before movement commands.
5. Rebuild after changing example source code.
6. Check the official [Unitree Document Center](https://support.unitree.com/home/zh/developer) for robot-specific network setup.

## Useful links

- [`unitreerobotics/unitree_sdk2`](https://github.com/unitreerobotics/unitree_sdk2)
- [`example/go2`](https://github.com/unitreerobotics/unitree_sdk2/tree/main/example/go2)
- [`example/g1`](https://github.com/unitreerobotics/unitree_sdk2/tree/main/example/g1)
- [Unitree Document Center](https://support.unitree.com/home/zh/developer)
