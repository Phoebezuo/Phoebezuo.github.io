---
layout:     post
title:      Unitree SDK2 Setup for Go2 and G1
date:       2026-05-31
summary:    Step by step notes for using unitree_sdk2 and Linux to connect with Unitree Go2 or G1 robots
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

Connect your computer to the robot by Ethernet.

Before checking the network, start both the controller and the robot.

Once the robot is powered on and in a safe position (hung up or lying on the ground), find the computer's network interface name:

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

If the Ethernet adapter is not connected to the robot correctly, the adapter may show `NO-CARRIER`, `state DOWN`, and no robot-network IP address:

![Bad ip addr example: Ethernet adapter is down and the robot is not detected](/images/unitree-sdk2/go2-ip-addr-bad.png)

When the Ethernet adapter is connected correctly, it should show `UP` and an IP address on the Unitree robot network, such as `192.168.123.222/24`:

![Good ip addr example: Ethernet adapter is up with 192.168.123.222 on the robot network](/images/unitree-sdk2/go2-ip-addr-good.png)

> In the commands below, replace `<network_interface>` with your real interface name.

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

Before running the SDK example, check the IP address on the robot-connected interface:

```bash
ip addr show <network_interface>
```

You should see:

```text
192.168.123.222/24
```

Then test the robot connection:

```bash
ping 192.168.123.161
```

If the connection is working, you should see packets being transmitted and replies coming back.

## Step 6: Connect with Go2

From the `unitree_sdk2/build` directory, find the Go2 example executables:

```bash
find . -type f -executable | grep -i go2
```

Then run the example with your robot network interface:

```bash
./path/to/example <network_interface>
```

For example:

```bash
./bin/go2_stand_example <network_interface>
```

Only run examples that match your robot model and test setup.

## Step 7: Connect with G1

From the `unitree_sdk2/build` directory, find the G1 example executables:

```bash
find . -type f -executable | grep -i g1
```

Then run the example with your robot network interface:

```bash
./path/to/example <network_interface>
```

For example:

```bash
./bin/g1_ankle_swing_example <network_interface>
```

Only run examples that match your robot model and test setup. A humanoid robot can fall, so make sure the robot is in a safe test space and follow Unitree's safety instructions.

## Step 8: Know which examples to use first

For Go2, useful examples include:

- `go2_sport_client`: high-level sport control
- `go2_robot_state_client`: robot state query
- `go2_video_client`: video client
- `go2_vui_client`: voice/user interaction client
- `go2_trajectory_follow`: trajectory follow example
- `go2_stand_example`: stand example
- `go2_low_level`: low-level control

For G1, useful example groups include:

- `g1/high_level`: high-level locomotion examples
- `g1/low_level`: low-level motion examples
- `g1/audio`: audio client examples
- `g1/dex3`: Dex3 hand examples
- `g1/g1d`: G1D examples

## Useful links

- [`unitreerobotics/unitree_sdk2`](https://github.com/unitreerobotics/unitree_sdk2)
- [`example/go2`](https://github.com/unitreerobotics/unitree_sdk2/tree/main/example/go2)
- [`example/g1`](https://github.com/unitreerobotics/unitree_sdk2/tree/main/example/g1)
- [Unitree Document Center](https://support.unitree.com/home/zh/developer)
