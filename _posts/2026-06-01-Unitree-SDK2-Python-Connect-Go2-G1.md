---
layout:     post
title:      Unitree SDK2 Python Setup for Go2 and G1
date:       2026-06-01
summary:    Step by step notes for using unitree_sdk2_python and Mac to connect with Unitree Go2 or G1 robots
categories: Robotics Unitree SDK
---

This note explains how to use [`unitree_sdk2_python`](https://github.com/unitreerobotics/unitree_sdk2_python) on Mac to connect with a Unitree Go2 or G1 robot.

The Python SDK is easier to try on Mac than the C++ SDK, but it still talks to the robot through DDS. That means two things matter:

1. install `unitree_sdk2_python` and CycloneDDS correctly
2. make sure your Mac is on the same network as the robot

## Step 1: Install basic tools on Mac

Install Homebrew first if you do not already have it:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Then install the tools needed to build CycloneDDS and run the SDK:

```bash
brew install git cmake python
```

Check Python:

```bash
python3 --version
python3 -m pip --version
```

The SDK requires Python 3.8 or newer.

## Step 2: Build CycloneDDS

The Python SDK depends on `cyclonedds==0.10.2`. If `pip install -e .` cannot find CycloneDDS, build CycloneDDS first.

```bash
cd ~
git clone https://github.com/eclipse-cyclonedds/cyclonedds -b releases/0.10.x
cd cyclonedds
mkdir build install
cd build
cmake .. -DCMAKE_INSTALL_PREFIX=../install
cmake --build . --target install
```

Set `CYCLONEDDS_HOME` to the install path:

```bash
export CYCLONEDDS_HOME="$HOME/cyclonedds/install"
```

To keep this setting after restarting terminal, add it to `~/.zshrc`:

```bash
echo 'export CYCLONEDDS_HOME="$HOME/cyclonedds/install"' >> ~/.zshrc
source ~/.zshrc
```

Check the install:

```bash
ls "$CYCLONEDDS_HOME"
ls "$CYCLONEDDS_HOME/lib"
ls "$CYCLONEDDS_HOME/include"
```

If those folders do not exist, the SDK install will probably fail.

## Step 3: Clone the Python SDK

```bash
cd ~
git clone https://github.com/unitreerobotics/unitree_sdk2_python.git
cd unitree_sdk2_python
```

## Step 4: Install the Python SDK

From the `unitree_sdk2_python` folder:

```bash
python3 -m pip install -e .
```

If you see this error:

```text
Could not locate cyclonedds. Try to set CYCLONEDDS_HOME or CMAKE_PREFIX_PATH
```

then check that `CYCLONEDDS_HOME` is set correctly:

```bash
echo "$CYCLONEDDS_HOME"
ls "$CYCLONEDDS_HOME/lib"
ls "$CYCLONEDDS_HOME/include"
```

Then run the install again:

```bash
python3 -m pip install -e .
```

## Step 5: Test DDS locally first

Before connecting to the robot, test the local publisher and subscriber examples.

Open one terminal:

```bash
cd ~/unitree_sdk2_python
python3 ./example/helloworld/publisher.py
```

Open another terminal:

```bash
cd ~/unitree_sdk2_python
python3 ./example/helloworld/subscriber.py
```

If the subscriber prints messages from the publisher, the Python SDK and DDS layer are working locally.

## Step 6: Connect the Mac to the robot network

Connect your Mac to the robot with Ethernet, usually through a USB-C to Ethernet adapter.

Find the network device name:

```bash
networksetup -listallhardwareports
```

Look for the Ethernet adapter. It may look like:

```text
Hardware Port: USB 10/100/1000 LAN
Device: en5
Ethernet Address: xx:xx:xx:xx:xx:xx
```

> In the commands below, replace `<network_interface>` with your real interface name, such as `en5`.

## Step 7: Configure the Mac IP if needed

Check the Ethernet interface:

```bash
ifconfig <network_interface>
```

If the interface already has an IP like this, you can skip manual IP configuration:

```text
inet 192.168.123.xxx netmask 0xffffff00
```

This diagram shows the full Mac check: find the Ethernet device with `networksetup`, check it with `ifconfig`, set the `192.168.123.222` IP if needed, and confirm the robot network:

![Mac robot network setup with networksetup, ifconfig, and Unitree robot IP checks](/images/unitree-sdk2/mac-robot-network-ifconfig.png)

If it has no `inet` address, or it has a different network like `192.168.1.xxx`, set a manual IP address:

```bash
sudo ifconfig <network_interface> inet 192.168.123.222 netmask 255.255.255.0 up
```

This means:

1. use this Ethernet adapter
2. set your Mac's IP to `192.168.123.222`
3. use subnet mask `255.255.255.0`
4. turn the adapter on

The robot and your Mac must be in the same `192.168.123.x` network for the SDK examples to communicate.

Then test that the Mac can reach the robot:

```bash
ping 192.168.123.161
```

If the connection is working, you should see replies from `192.168.123.161`.

## Step 8: Connect with Go2

For Go2, start with the high-level sport client example:

```bash
cd ~/unitree_sdk2_python
python3 ./example/go2/high_level/go2_sport_client.py <network_interface>
```

Example:

```bash
python3 ./example/go2/high_level/go2_sport_client.py en5
```

The example is interactive. Type `list` to see available test options. Common options include:

```text
damp
stand_up
stand_down
move forward
move lateral
move rotate
stop_move
balanced stand
recovery
```

Start with `stand_up`, `stand_down`, `balanced stand`, or `recovery`. Do not start with movement options unless the robot has enough open space.

## Step 9: Connect with G1

For G1, use the G1 high-level loco client example:

```bash
cd ~/unitree_sdk2_python
python3 ./example/g1/high_level/g1_loco_client_example.py <network_interface>
```

Example:

```bash
python3 ./example/g1/high_level/g1_loco_client_example.py en5
```

The example is interactive. It asks you to confirm that the robot has no obstacles around it, then you can type `list` to see available test options.

Use simple state or stand/balance options first. Be careful with movement commands because G1 is a humanoid robot and can fall.

## Step 10: Know which examples to use first

For Go2:

- `example/go2/high_level/go2_sport_client.py`: high-level sport control
- `example/go2/high_level/go2_utlidar_switch.py`: LiDAR switch
- `example/go2/front_camera/camera_opencv.py`: front camera through OpenCV
- `example/go2/front_camera/capture_image.py`: capture one image from the front camera
- `example/wireless_controller/wireless_controller.py`: read controller state
- `example/obstacles_avoid/obstacles_avoid_switch.py`: obstacle avoidance switch
- `example/vui_client/vui_client_example.py`: light and volume control

For G1:

- `example/g1/high_level/g1_loco_client_example.py`: high-level locomotion client
- `example/g1/high_level/g1_arm5_sdk_dds_example.py`: 5-DoF arm example
- `example/g1/high_level/g1_arm7_sdk_dds_example.py`: 7-DoF arm example
- `example/g1/audio/g1_audio_client_example.py`: audio client
- `example/g1/low_level/g1_ankle_swing_example.py`: low-level ankle example

For first connection tests, use high-level examples before low-level examples.

## Step 11: Basic troubleshooting

If `pip install -e .` fails:

1. check `python3 --version`
2. check `echo "$CYCLONEDDS_HOME"`
3. check `ls "$CYCLONEDDS_HOME/lib"`
4. check `ls "$CYCLONEDDS_HOME/include"`
5. run `python3 -m pip install -e .` again from `~/unitree_sdk2_python`

If the robot example cannot connect:

1. check the Ethernet interface with `networksetup -listallhardwareports`
2. check the IP address with `ifconfig <network_interface>`
3. make sure the Mac IP is `192.168.123.xxx`
4. make sure you pass the same interface name to the Python example
5. try a safe high-level option like `damp`, `stand_up`, or `balanced stand` before movement control
6. check the official Unitree network setup document for your robot

## Useful links

- [`unitreerobotics/unitree_sdk2_python`](https://github.com/unitreerobotics/unitree_sdk2_python)
- [`example` folder](https://github.com/unitreerobotics/unitree_sdk2_python/tree/master/example)
- [Unitree Developer Quick Start](https://support.unitree.com/home/en/developer/Quick_start)
- [CycloneDDS install notes](https://pypi.org/project/cyclonedds/)
