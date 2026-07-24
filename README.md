<div align="center">
  <h1 align="center">xr_teleoperate</h1>
  <a href="https://www.unitree.com/" target="_blank">
    <img src="https://www.unitree.com/images/0079f8938336436e955ea3a98c4e1e59.svg" alt="Unitree LOGO" width="15%">
  </a>
  <p align="center">
    <a href="https://github.com/unitreerobotics/xr_teleoperate/wiki" target="_blank"> <img src="https://img.shields.io/badge/GitHub-Wiki-181717?logo=github" alt="Unitree LOGO"></a> <a href="https://discord.gg/ZwcVwxv5rq" target="_blank"><img src="https://img.shields.io/badge/-Discord-5865F2?style=flat&logo=Discord&logoColor=white" alt="Unitree LOGO"> <a href="https://deepwiki.com/unitreerobotics/xr_teleoperate"><img src="https://deepwiki.com/badge.svg" alt="Ask DeepWiki"></a> </a>
  </p>
</div>


# 📺 Video Demo

<p align="center">
  <table>
    <tr>
      <td align="center" width="50%">
        <a href="https://www.youtube.com/watch?v=OTWHXTu09wE" target="_blank">
          <img src="https://img.youtube.com/vi/OTWHXTu09wE/maxresdefault.jpg" alt="Video 1" width="75%">
        </a>
        <p><b> G1 (29DoF) + Dex3-1 </b></p>
      </td>
      <td align="center" width="50%">
        <a href="https://www.youtube.com/watch?v=pNjr2f_XHoo" target="_blank">
          <img src="https://img.youtube.com/vi/pNjr2f_XHoo/maxresdefault.jpg" alt="Video 2" width="75%">
        </a>
        <p><b> H1_2 (Arm 7DoF) </b></p>
      </td>
    </tr>
  </table>
</p>


# 🔖[Release Note](CHANGELOG.md)

## 🏷️ v1.5 (2025.12.29)

- support simulation
- add CycloneDDS interface name parameter
- [add caching to speed-up urdf loading](https://github.com/unitreerobotics/xr_teleoperate/commit/6cab654620735bfa347c1cd32a0d8c0c1e6ec343)
- ...



# 0. 📖 Introduction

The currently supported devices in this repository:

<table>
  <tr>
    <th align="center">🤖 Robot</th>
    <th align="center">⚪ Status</th>
  </tr>
  <tr>
    <td align="center"><a href="https://www.unitree.com/g1" target="_blank">G1 (29 DoF)</a></td>
    <td align="center">✅ Complete</td>
  </tr>
  <tr>
    <td align="center"><a href="https://www.unitree.com/g1" target="_blank">G1 (23 DoF)</a></td>
    <td align="center">✅ Complete</td>
  </tr>
  <tr>
    <td align="center"><a href="https://www.unitree.com/h1" target="_blank">H1 (4‑DoF arm)</a></td>
    <td align="center">✅ Complete</td>
  </tr>
  <tr>
    <td align="center"><a href="https://www.unitree.com/h1" target="_blank">H1_2 (7‑DoF arm)</a></td>
    <td align="center">✅ Complete</td>
  </tr>
  <tr>
    <td align="center"><a href="https://www.unitree.com/h2" target="_blank">H2 (7‑DoF arm)</a></td>
    <td align="center">✅ Complete</td>
  </tr>
  <tr>
    <td align="center"><a href="https://www.unitree.com/Dex1-1" target="_blank">Dex1‑1 gripper</a></td>
    <td align="center">✅ Complete</td>
  </tr>
  <tr>
    <td align="center"><a href="https://www.unitree.com/Dex3-1" target="_blank">Dex3‑1 dexterous hand</a></td>
    <td align="center">✅ Complete</td>
  </tr>
  <tr>
    <td align="center"><a href="https://support.unitree.com/home/en/G1_developer/inspire_dfx_dexterous_hand" target="_blank">Inspire dexterous hand</a></td>
    <td align="center">✅ Complete</td>
  </tr>
  <tr>
    <td style="text-align: center;"> <a href="https://www.brainco-hz.com/docs/revolimb-hand/" target="_blank"> BrainCo dexterous hand </td>
    <td style="text-align: center;"> &#9989; Complete </td>
  </tr>
  <tr>
    <td align="center"> ··· </td>
    <td align="center"> ··· </td>
  </tr>
</table>



# 1. 📦 Installation
This document shows how to install the xr_teleoperate project onto a real G1/G1D. 
All the commands are run on the G1/G1D PC2.

If you have troubles installing this project, this link may be helpful.
https://serviceconsole.unitree.com/#/help/03020402

If you want to do experiment in simulation rather than a real G1/G1D, please refer to the unitree official webpage:

https://github.com/unitreerobotics/xr_teleoperate

## 1.1 📥 basic

```bash
# Create a conda environment
## 适用于jetson orin nx（ARM架构）
unitree@PC2:~$ mkdir -p ~/miniconda3
unitree@PC2:~$ wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-aarch64.sh -O ~/miniconda3/miniconda.sh
unitree@PC2:~$ bash ~/miniconda3/miniconda.sh -b -u -p ~/miniconda3
unitree@PC2:~$ rm ~/miniconda3/miniconda.sh
unitree@PC2:~$ source ~/miniconda3/bin/activate
(base) unitree@PC2:~$ conda init --all
# 创建 conda 基础环境
(base) unitree@PC2:~$ conda create -n tv python=3.10 pinocchio=3.1.0 numpy=1.26.4 -c conda-forge
(base) unitree@PC2:~$ conda activate tv

# Clone this repo
(tv) unitree@PC2:~$ git clone https://github.com/unitreerobotics/xr_teleoperate.git
(tv) unitree@PC2:~$ cd xr_teleoperate
# Shallow clone submodule
(tv) unitree@PC2:~/xr_teleoperate$ git submodule update --init --depth 1
```

```bash
# Install teleimager submodule
(tv) unitree@PC2:~/xr_teleoperate$ sudo apt install -y libusb-1.0-0-dev libturbojpeg-dev
(tv) unitree@PC2:~/xr_teleoperate$ cd teleop/teleimager
(tv) unitree@PC2:~/xr_teleoperate/teleop/teleimager$ pip install -e
(tv) unitree@PC2:~/xr_teleoperate/teleop/teleimager$ pip install -e ".[server]"
# 添加 video 权限（非 root 用户运行）：
(tv) unitree@PC2:~/xr_teleoperate/teleop/teleimager$ bash setup_uvc.sh
## if you need realsensse ↓↓↓
(tv) unitree@PC2:~/xr_teleoperate/teleop/teleimager$ conda install conda-forge::pyrealsense2
```

```bash
# Install televuer submodule
(tv) unitree@PC2:~/xr_teleoperate$ cd teleop/televuer
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ pip install -e .
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ pip install params_proto==2.13.2  vuer==0.0.60
```

```bash
# Install dex-retargeting submodule
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ cd ../robot_control/dex-retargeting/
(tv) unitree@PC2:~/xr_teleoperate/teleop/robot_control/dex-retargeting$ pip install "numpy==1.26.4" "torch==2.3.0" "pytransform3d>=3.5.0" "pin>=2.7.0" "trimesh>=4.4.0" "anytree>=2.12.0" "pyyaml>=6.0.0" "lxml>=5.2.2"
(tv) unitree@PC2:~/xr_teleoperate/teleop/robot_control/dex-retargeting$ conda install conda-forge::nlopt
(tv) unitree@PC2:~/xr_teleoperate/teleop/robot_control/dex-retargeting$ pip install -e . --no-deps
```

```bash
# Install other necessary libs
(tv) unitree@PC2:~/xr_teleoperate/teleop/robot_control/dex-retargeting$ cd ../../../
(tv) unitree@PC2:~/xr_teleoperate$ pip install -r requirements.txt
```

```bash
# Configure SSL certificates for the televuer module so that XR devices (e.g., Pico / Quest / Apple Vision Pro) can securely connect via HTTPS / WebRTC
# 1. Generate certificate files
# 1.1 For Pico / Quest XR devices
(tv) unitree@PC2:~$ cd ~/xr_teleoperate/teleop/televuer
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout key.pem -out cert.pem
#Country Name (2 letter code) [AU]:JP
#State or Province Name (full name) [Some-State]:Tokyo
#Locality Name (eg, city) []:Koto
#Organization Name (eg, company) [Internet Widgits Pty Ltd]:TechShare
#Organizational Unit Name (eg, section) []:
#Common Name (e.g. server FQDN or YOUR name) []:localhost
#Email Address []:

# 1.2 For Apple Vision Pro
(tv) unitree@PC2:~$ cd ~/xr_teleoperate/teleop/televuer
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ openssl genrsa -out rootCA.key 2048
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ openssl req -x509 -new -nodes -key rootCA.key -sha256 -days 365 -out rootCA.pem -subj "/CN=xr-teleoperate"
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ openssl genrsa -out key.pem 2048
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ openssl req -new -key key.pem -out server.csr -subj "/CN=localhost"
# Create server_ext.cnf file with the following content (IP.2 should match your host IP, e.g., 192.168.123.2. Use ifconfig or similar to check)
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ vim server_ext.cnf
subjectAltName = @alt_names
[alt_names]
DNS.1 = localhost
IP.1 = 192.168.123.164
IP.2 = 192.168.123.2
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ openssl x509 -req -in server.csr -CA rootCA.pem -CAkey rootCA.key -CAcreateserial -out cert.pem -days 365 -sha256 -extfile server_ext.cnf
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ ls
build  cert.pem  key.pem  LICENSE  pyproject.toml  README.md  rootCA.key  rootCA.pem  rootCA.srl  server.csr  server_ext.cnf  src  test
# Copy rootCA.pem to Apple Vision Pro via AirDrop and install it

# 1.3 Enable firewall， for both apple and Pico / Quest XR devices
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ sudo ufw allow 8012

# 2. Configure certificate paths, choose one method
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ mkdir -p ~/.config/xr_teleoperate/
(tv) unitree@PC2:~/xr_teleoperate/teleop/televuer$ cp cert.pem key.pem ~/.config/xr_teleoperate/
```



## 1.2 🕹️ unitree_sdk2_python
```bash
# 情况1： 默认情况下，G1自带了cyclonedds_ws，此时可以直接安装unitree_sdk2_python
(tv) unitree@PC2:~$ git clone https://github.com/unitreerobotics/unitree_sdk2_python.git
(tv) unitree@PC2:~$ cd unitree_sdk2_python
(tv) unitree@PC2:~$ export CYCLONEDDS_HOME=~/cyclonedds_ws/install/cyclonedds
(tv) unitree@PC2:~/unitree_sdk2_python$ pip install -e .

```

```bash
# 情况2： 如果G1没有自带cyclonedds_ws，需要手动安装cyclonedds，再安装unitree_sdk2_python
cd ~
git clone https://github.com/eclipse-cyclonedds/cyclonedds -b releases/0.10.x 
cd cyclonedds && mkdir build install && cd build
cmake .. -DCMAKE_INSTALL_PREFIX=../install
cmake --build . --target install

(tv) unitree@PC2:~$ git clone https://github.com/unitreerobotics/unitree_sdk2_python.git
(tv) unitree@PC2:~$ cd unitree_sdk2_python
(tv) unitree@PC2:~$ export CYCLONEDDS_HOME=~/cyclonedds/install
(tv) unitree@PC2:~/unitree_sdk2_python$ pip install -e .
```


## 1.3 🖼️ Image Service
1. 查找已连接的摄像头
   ```bash
   ## 如果摄像头存在 RealSense 设备需加上 --rs 参数，就会看到 RealSense 摄像头的搜索结果，反之为普通USB摄像头不需要加上 --rs 参数
   # G1头部摄像头存在RealSense设备，需要加上--rs参数
   (tv) unitree@ubuntu:~$ teleimager-server --cf --rs
   
   # 普通USB摄像头，用以下命令搜索
   (tv) unitree@ubuntu:~$ teleimager-server --cf
   ```
   
   ```bash
   (tv) unitree@ubuntu:~$ teleimager-server --cf --rs
   11:44:58.245700 INFO     [Performance] CPU Affinity locked to: [0, 1, 2]                                    image_server.py:1487
   11:44:58.261900 ERROR    Failed to reload driver: Command 'sudo modprobe -r uvcvideo' returned non-zero exit image_server.py:544
                           status 1.                                                                                              
   11:45:01.913952 INFO     ======================= Camera Discovery Start ==================================   image_server.py:788
   11:45:01.914496 INFO     Found video devices: ['/dev/video0', '/dev/video1', '/dev/video2', '/dev/video3',   image_server.py:789
                           '/dev/video4', '/dev/video5', '/dev/video6', '/dev/video7', '/dev/video8']   
   11:45:01.915579 INFO     Found RGB video devices: ['/dev/video6', '/dev/video8']                             image_server.py:790
   11:45:01.915793 INFO     ----------------------- Realsense Cameras ----------------------------------        image_server.py:793
   11:45:01.915988 INFO     RealSense serial numbers: ['243322070193']                                          image_server.py:794
   11:45:01.916173 INFO     RealSense video paths: ['/dev/video0', '/dev/video1', '/dev/video2', '/dev/video3', image_server.py:795
                           '/dev/video4', '/dev/video5']                                                                          
   11:45:01.916350 INFO     RealSense RGB-like video paths: ['/dev/video2']                                     image_server.py:796
   11:45:01.916537 INFO     ----------------------- OpenCV / UVC Camera 1 -----------------------------         image_server.py:799
   11:45:01.916951 INFO     video_path    : /dev/video6                                                         image_server.py:800
   11:45:01.917252 INFO     video_id      : 6                                                                   image_server.py:801
   11:45:01.917341 INFO     serial_number : 0001                                                                image_server.py:802
   11:45:01.917426 INFO     physical_path : /sys/devices/platform/3610000.xhci/usb1/1-2/1-2.2/1-2.2:1.0         image_server.py:803
   11:45:01.917517 INFO     extra_info:                                                                         image_server.py:804
   11:45:01.917598 INFO         name: 0001                                                                      image_server.py:811
   11:45:01.917677 INFO         manufacturer: JSK-WDR                                                           image_server.py:811
   11:45:01.918148 INFO         uid: 1:5                                                                        image_server.py:811
   11:45:02.075066 INFO         format: 480x640@30 MJPG                                                         image_server.py:816
   11:45:02.077378 INFO         format: 1080x1920@60 MJPG                                                       image_server.py:816
   11:45:02.104215 INFO     ----------------------- OpenCV / UVC Camera 2 -----------------------------         image_server.py:799
   11:45:02.104594 INFO     video_path    : /dev/video8                                                         image_server.py:800
   11:45:02.104711 INFO     video_id      : 8                                                                   image_server.py:801
   11:45:02.104810 INFO     serial_number : 0002                                                                image_server.py:802
   11:45:02.104902 INFO     physical_path : /sys/devices/platform/3610000.xhci/usb1/1-2/1-2.3/1-2.3:1.0         image_server.py:803
   11:45:02.104991 INFO     extra_info:                                                                         image_server.py:804
   11:45:02.105077 INFO         name: 0002                                                                      image_server.py:811
   11:45:02.105162 INFO         manufacturer: JSK-WDR                                                           image_server.py:811
   11:45:02.105618 INFO         uid: 1:6                                                                        image_server.py:811
   11:45:02.267168 INFO         format: 480x640@30 MJPG                                                         image_server.py:816
   11:45:02.269074 INFO         format: 1080x1920@60 MJPG                                                       image_server.py:816
   11:45:02.288887 INFO     =========================== Camera Discovery End ================================   image_server.py:824
      
   ```

2. 配置cam_config_server.yaml文件

   根据上一步搜索到的摄像头结果配置/home/unitree/xr_teleoperate/teleop/teleimager/cam_config_server.yaml
   若头部摄像头和左右手的摄像头都有，无法确定id是哪个摄像头的，可以把其他摄像头拔掉，一次只接入一个摄像头并重新用上一步骤查找id（第一次只接入头部摄像头，第二次只接入左腕摄像头，以此类推）
   ```bash
   # 使用vim编辑cam_config_server.yaml
   (tv) unitree@ubuntu:~$ cd xr_teleoperate/teleop/teleimager/
   (tv) unitree@ubuntu:~/xr_teleoperate/teleop/teleimager$ vim cam_config_server.yaml
   ```

   ```bash
   ## 注意：文件里面有需要变动的部分会用中文注释来提示，请根据实际情况进行修改
   # =====================================================
   # Head camera configuration
   # =====================================================
   # camera topic
   head_camera:
     # camera config
   
     # if enable_zmq and enable_webrtc are both false, the camera will not start
     # Set to true to enable ZMQ publishing, false to disable
     enable_zmq: true
     # Port to publish camera stream, e.g. zmq tcp://*:55555.  image_client.py should connect to the same port
     zmq_port : 55555
     # Set to true to enable WebRTC publishing, false to disable
     enable_webrtc: true
     # Port for WebRTC signaling server
     webrtc_port : 60001
     # webrtc codec preference, options: "vp8", "h264"
     webrtc_codec: h264
   
     # Type of camera:
     #   - "opencv"    → opencv driver
     #   - "realsense" → pyrealsense2 driver
     #   - "uvc"       → pyuvc driver
     type: realsense # 根据G1头部摄像头情况修改，一般情况用realsense
   
     # Image Format
     # image resolution: [height, width]
     image_shape: [480, 640] # 根据G1头部摄像头支持的分辨率情况修改
     binocular: false # 用双目的话图像显示有问题，需改成false
     # frame per second
     fps: 30
   
     # Camera identifiers (choose one or more):
     #   - video_id: X        → /dev/videoX  (e.g. 0 → /dev/video0)
     #   - serial_number: Y   → camera's hardware serial (e.g. 141722079879)
     #   - physical_path: Z   → sysfs physical USB path (e.g. /sys/devices/pci0000:00/.../1-11.2:1.0)
     #
     # Identifier priority:
     #   physical_path > serial_number > video_id
     #   if an identifier is not used, set it to null. The system will resolve the camera by priority.
     #
     # Notes:
     #   - type "realsense": supports serial_number only (but a RealSense can also be used as opencv/uvc if desired)
     #   - type "opencv":    supports video_id, serial_number, physical_path
     #   - type "uvc":       supports video_id, serial_number, physical_path
     video_id: null # RealSense摄像头不需要指定该参数，使用null
     serial_number: "243322070193" # 修改为1.3.1查找到的RealSense serial numbers，需用双引号括起来
     physical_path: null # RealSense摄像头不需要指定该参数，使用null
   
   # =====================================================
   # Left wrist camera configuration
   # =====================================================
   left_wrist_camera:
     enable_zmq: false # 有安装左腕摄像头则为true，反之为false
     zmq_port : 55556
     enable_webrtc: false # 有安装左腕摄像头则为true，反之为false
     webrtc_port : 60002
     webrtc_codec: h264
     type: uvc # 若左腕摄像头是RealSense设备则修改为realsense，反之为uvc
     image_shape: [480, 640]
     binocular: false # 双目摄像头则用true，反之为false
     fps: 30
     video_id: 2 # 修改为1.3.1查找到的video_id，没有则为null
     serial_number: "200901010001" # 修改为1.3.1查找到的serial_number，没有则为null
     physical_path: null # 修改为1.3.1查找到的physical_path，没有则为null
   
   # =====================================================
   # Right wrist camera configuration
   # =====================================================
   right_wrist_camera:
     enable_zmq: false # 有安装右腕摄像头则为true，反之为false
     zmq_port : 55557
     enable_webrtc: false # 有安装右腕摄像头则为true，反之为false
     webrtc_port: 60003
     webrtc_codec: h264
     type: uvc # 若右腕摄像头是RealSense设备则修改为realsense，反之为uvc
     image_shape: [480, 640]
     binocular: false # 双目摄像头则用true，反之为false
     fps: 30
     video_id: 4 # 修改为1.3.1查找到的video_id，没有则为null
     serial_number: "200901010002" # 修改为1.3.1查找到的serial_number，没有则为null
     physical_path: null # 修改为1.3.1查找到的physical_path，没有则为null
   ```
   
3. 启动并测试图像服务器

   ```bash
   # 若使用了RealSense摄像头
   (tv) unitree@ubuntu:~$ teleimager-server --rs
   
   # 若没有使用RealSense摄像头
   (tv) unitree@ubuntu:~$ teleimager-server 
   ```
   
   ```bash
   # 使用WebRTC方式测试图像服务器,注意避免使用火狐浏览器，推荐谷歌浏览器
   https://<host_ip>:<webrtc_port>
   # 例如
   https://192.168.123.164:60001
   # 点击 start 按钮，若配置正常，则可以看到头部摄像头画面
   # 如有手腕摄像头，以下地址可以查看手腕摄像头画面
   https://192.168.123.164:60002
   https://192.168.123.164:60003
   ```
   ```bash
   # 完成上述配置并测试成功后，可以通过以下脚本配置系统自动启动图像服务：
   (tv) unitree@ubuntu:~/xr_teleoperate/teleop/teleimager$ bash setup_autostart.sh
   ```

   
# 2. ✋ Hands (optional)
## 2.1 ✋ Inspire Hand Service (optional)

> **Note 1**: Skip this if your config does not use the Inspire hand.
>
> **Note 2**: For G1 robot with [Inspire DFX hand](https://support.unitree.com/home/zh/G1_developer/inspire_dfx_dexterous_hand), related issue [#46](https://github.com/unitreerobotics/xr_teleoperate/issues/46).
>
> **Note 3**: For [Inspire FTP hand]((https://support.unitree.com/home/zh/G1_developer/inspire_ftp_dexterity_hand)), related issue [#48](https://github.com/unitreerobotics/xr_teleoperate/issues/48). FTP dexterous hand is now supported. Please refer to the `--ee` parameter for configuration.

First, use [this URL: DFX_inspire_service](https://github.com/unitreerobotics/DFX_inspire_service) to clone the dexterous hand control interface program. And Copy it to **PC2** of  Unitree robots. 

On Unitree robot's **PC2**, execute command:

```bash
unitree@PC2:~$ sudo apt install libboost-all-dev libspdlog-dev
# Build project
unitree@PC2:~$ cd DFX_inspire_service && mkdir build && cd build
unitree@PC2:~/DFX_inspire_service/build$ cmake ..
unitree@PC2:~/DFX_inspire_service/build$ make -j6

# (For unitree g1) Terminal 1.
unitree@PC2:~/DFX_inspire_service/build$ sudo ./inspire_g1
# or (For unitree h1) Terminal 1.
unitree@PC2:~/DFX_inspire_service/build$ sudo ./inspire_h1 -s /dev/ttyUSB0

# Terminal 2. Run example
unitree@PC2:~/DFX_inspire_service/build$ ./hand_example
```

If two hands open and close continuously, it indicates success. Once successful, close the `./hand_example` program in Terminal 2.



## 2.2 ✋ BrainCo Hand Service (Optional)

Please refer to the [Repo README](https://github.com/unitreerobotics/brainco_hand_service) for setup instructions.

## 2.3 ✋ Unitree Dex1_1 Service (Optional)

Please refer to the [Repo README](https://github.com/unitreerobotics/dex1_1_service) for setup instructions.

# 3 🚀 Launch
## 3.1 🚀 Launch Parameter Description

- **Basic control parameters**

|      ⚙️ Parameter      |                        📜 Description                         |                     🔘 Available Options                      |     📌 Default     |
| :-------------------: | :----------------------------------------------------------: | :----------------------------------------------------------: | :---------------: |
|     `--frequency`     |            Set the FPS for recording and control             |                  Any reasonable float value                  |       30.0        |
|    `--input-mode`     |       Choose XR input mode (how to control the robot)        |   `hand` (hand tracking)`controller` (controller tracking)   |      `hand`       |
|   `--display-mode`    |  Choose XR display mode (how to view the robot perspective)  | `immersive` (immersive)`ego` (pass-through + small first-person window)`pass-through` (pass-through only) |    `immersive`    |
|        `--arm`        |      Select the robot arm type (see 0. 📖 Introduction)       |                 `G1_29` `G1_23` `H1_2` `H1`                  |      `G1_29`      |
|        `--ee`         | Select the end-effector type of the arm (see 0. 📖 Introduction) |     `dex1` `dex3` `inspire_ftp` `inspire_dfx` `brainco`      |       None        |
|   `--img-server-ip`   | Set the image server IP address for receiving image streams and configuring WebRTC signaling |                        `IPv4` address                        | `192.168.123.164` |
| `--network-interface` |    Set the network interface for CycloneDDS communication    |                    Network Interface Name                    |      `None`       |

- **Mode switch parameters**

| ⚙️ Parameter  |                        📜 Description                         |
| :----------: | :----------------------------------------------------------: |
|  `--motion`  | **Enable motion control mode** When enabled, the teleoperation program can run alongside the robot’s motion control program.In **hand tracking** mode, the [R3 controller](https://www.unitree.com/cn/R3) can be used to control normal robot walking; in **controller tracking** mode, joysticks can also control the robot’s movement.<br />Note: Only `Regular mode` (R1+X) is supported, `Running mode` (R2+A) is not supported. |
| `--headless` | **Enable headless mode** For running the program on devices without a display, e.g., the Development Computing Unit (PC2). |
|   `--sim`    | **Enable [simulation mode](https://github.com/unitreerobotics/unitree_sim_isaaclab)** |
|   `--ipc`    | **Inter-process communication mode** Allows controlling the xr_teleoperate program’s state via IPC. Suitable for interaction with agent programs. |
| `--affinity` | **CPU affinity mode** Set CPU core affinity. If you are unsure what this is, do not set it. |
|  `--record`  | **Enable data recording mode** Press **r** to start teleoperation, then **s** to start recording; press **s** again to stop and save the episode. Press **s** repeatedly to repeat the process. |
|  `--task-*`  | Configure the save path, target, description, and steps of the recorded task. |


>  ![Warning](https://img.shields.io/badge/Warning-Important-red)
>
>  1. Everyone must keep a safe distance from the robot to prevent any potential danger!
>  2. Please make sure to read the [Official Documentation](https://support.unitree.com/home/zh/Teleoperation) at least once before running this program.
>  3. To use motion mode (with `--motion`), ensure the robot is in control mode (via [R3 remote](https://www.unitree.com/R3)).
>  5. In motion mode:
>    - Right controller **A** = Exit teleop
>    - Both joysticks pressed = soft emergency stop (switch to damping mode)
>    - Left joystick = drive directions; 
>    - right joystick = turning; 
>    - max speed is limited in the code.

Same as simulation but follow the safety warnings above.

## 3.2 🚀  Launch Command
1. 假设选择**手柄跟踪控制 G1(29 DoF)**进行遥操，同时开启数据录制模式。则启动命令如下所示：（根据实际情况选择）
   ```bash
   # 手柄跟踪控制 G1(29 DoF)
   (tv) unitree@ubuntu:~$ cd ~/xr_teleoperate/teleop/
   (tv) unitree@ubuntu:~/xr_teleoperate/teleop/$ python teleop_hand_and_arm.py --input-mode=controller --img-server-ip=192.168.1.100 --record
   # --img-server-ip为PC2和XR设备连接同一个WiFi的IP
   ```

   假设选择手柄跟踪控制 G1(29 DoF) + Dex1-1夹爪进行遥操，同时开启数据录制模式。则启动命令如下所示：（根据实际情况选择）
   ```bash
   ## 手柄跟踪控制 G1(29 DoF) + Dex1-1夹爪
   # 若需要控制Dex1-1的夹爪请查看宇树文档中心和B站教程对夹爪进行部署并设置为开机自启动
   # 1.文档中心链接：https://support.unitree.com/home/zh/dex1-1_gripper/dex1_1
   # 2.B站视频链接：https://www.bilibili.com/video/BV1BY9DB3EfW/?spm_id_from=333.337.search-card.all.click&vd_source=8d9d3245c455c9065923881e36fae6fb
   
   # 需要指定--ee=dex1即可控制夹爪，其他灵巧手也可参考该方式
   (tv) unitree@ubuntu:~$ cd ~/xr_teleoperate/teleop/
   (tv) unitree@ubuntu:~/xr_teleoperate/teleop/$ python teleop_hand_and_arm.py --input-mode=controller --ee=dex1 --img-server-ip=192.168.1.100 --record
   # --img-server-ip为PC2和XR设备连接同一个WiFi的IP
   ```
2. 程序正常启动后，终端输出信息如下图所示：
   After the program starts, the terminal shows:
   
   <p align="center">   <a href="https://oss-global-cdn.unitree.com/static/735464d237214f6c9edf8c7db9847a0a_1874x1275.png">     <img src="https://oss-global-cdn.unitree.com/static/735464d237214f6c9edf8c7db9847a0a_1874x1275.png" alt="Terminal Start Log" style="width: 75%;">   </a> </p>

3. 戴上您的 XR 头显设备（比如 apple vision pro 或 pico4 ultra enterprise等）

   连接对应的 WiFi 热点

   Open a browser (e.g. Safari or PICO Browser) and go to:  `https://192.168.123.2:8012/?ws=wss://192.168.123.2:8012`

   > **Note 1**: This IP must match your **Host** IP (check with `ifconfig`).
   > 
   > **Note 2**: Use `https://vuer.ai?ws=wss://192.168.123.2:8012` for PICO if the websocket connection cannot be set.
   > 
   > **Note 3**: You may see a warning page. Click **Advanced**, then **Proceed to IP (unsafe)**.

   <p align="center">
     <a href="https://oss-global-cdn.unitree.com/static/cef18751ca6643b683bfbea35fed8e7c_1279x1002.png">
       <img src="https://oss-global-cdn.unitree.com/static/cef18751ca6643b683bfbea35fed8e7c_1279x1002.png" alt="vuer_unsafe" style="width: 50%;">
     </a>
   </p>

4. In the Vuer web, click **Virtual Reality**. Allow all prompts to start the VR session.

   <p align="center">  <a href="https://oss-global-cdn.unitree.com/static/fdeee4e5197f416290d8fa9ecc0b28e6_2480x1286.png">    <img src="https://oss-global-cdn.unitree.com/static/fdeee4e5197f416290d8fa9ecc0b28e6_2480x1286.png" alt="Vuer UI" style="width: 75%;">  </a> </p>

   You’ll see the robot’s first-person view in the headset. The terminal prints connection info:

   ```bash
   websocket is connected. id:dbb8537d-a58c-4c57-b49d-cbb91bd25b90
   default socket worker is up, adding clientEvents
   Uplink task running. id:dbb8537d-a58c-4c57-b49d-cbb91bd25b90
   ```
5. Align your arm to the **robot’s initial pose** to avoid sudden movements at start:

   <p align="center">  <a href="https://oss-global-cdn.unitree.com/static/2522a83214744e7c8c425cc2679a84ec_670x867.png">    <img src="https://oss-global-cdn.unitree.com/static/2522a83214744e7c8c425cc2679a84ec_670x867.png" alt="Initial Pose" style="width: 25%;">  </a> </p>

6. Press **r** in the terminal to begin teleoperation. You can now control the robot arm and dexterous hand.

7. During teleoperation, press **s** to start recording; press **s** again to stop and save. Repeatable process.

<p align="center">  <a href="https://oss-global-cdn.unitree.com/static/f5b9b03df89e45ed8601b9a91adab37a_2397x1107.png">    <img src="https://oss-global-cdn.unitree.com/static/f5b9b03df89e45ed8601b9a91adab37a_2397x1107.png" alt="Recording Process" style="width: 75%;">  </a> </p>

> **Note 1**: Recorded data is stored in `xr_teleoperate/teleop/utils/data` by default, with usage instructions at this repo:  [unitree_IL_lerobot](https://github.com/unitreerobotics/unitree_IL_lerobot/tree/main?tab=readme-ov-file#data-collection-and-conversion).
>
> **Note 2**: Please pay attention to your disk space size during data recording.
>
> **Note 3**: In v1.4 and above, the “record image” window has been removed.




## 3.3 🔚 Exit

> ![Warning](https://img.shields.io/badge/Warning-Important-red)
>
> To avoid damaging the robot, it is recommended to position the robot's arms close to the initial pose before pressing **q** to exit.
>
> - In **Debug Mode**: After pressing the exit key, both arms will return to the robot's **initial pose** within 5 seconds, and then the control will end.
>
> - In **Motion Mode**: After pressing the exit key, both arms will return to the robot's **motion control pose** within 5 seconds, and then the control will end.

Same as simulation but follow the safety warnings above.



# 4. 🗺️ Codebase Overview

```
xr_teleoperate/
│
├── assets                    [Stores robot URDF-related files]
│
├── teleop
│   ├── teleimager            [New image service library, supporting multiple features]
│   │
│   ├── televuer
│   │      ├── src/televuer
│   │         ├── television.py       [Captures head, wrist, and hand/controller data from XR devices using Vuer]
│   │         ├── tv_wrapper.py       [Post-processing of captured data]
│   │      ├── test
│   │         ├── _test_television.py [Test program for television.py]
│   │         ├── _test_tv_wrapper.py [Test program for tv_wrapper.py]
│   │
│   ├── robot_control
│   │      ├── src/dex-retargeting [Dexterous hand retargeting algorithm library]
│   │      ├── robot_arm_ik.py     [Inverse kinematics for the arm]
│   │      ├── robot_arm.py        [Controls dual-arm joints and locks other parts]
│   │      ├── hand_retargeting.py [Wrapper for the dexterous hand retargeting library]
│   │      ├── robot_hand_inspire.py  [Controls Inspire dexterous hand]
│   │      ├── robot_hand_unitree.py  [Controls Unitree dexterous hand]
│   │
│   ├── utils
│   │      ├── episode_writer.py          [Used to record data for imitation learning]
│   │      ├── weighted_moving_filter.py  [Filter for joint data]
│   │      ├── rerun_visualizer.py        [Visualizes recorded data]
│   │      ├── ipc.py                     [Handles inter-process communication with proxy programs]
│   │      ├── motion_switcher.py         [Switches motion control states]
│   │      ├── sim_state_topic.py         [For simulation deployment]
│   │
│   └── teleop_hand_and_arm.py    [Startup script for teleoperation]

```

# 5. 🛠️ Hardware

please see [Device document](Device.md).



# 6. 🙏 Acknowledgement

This code builds upon following open-source code-bases. Please visit the URLs to see the respective LICENSES:

1. https://github.com/OpenTeleVision/TeleVision
2. https://github.com/dexsuite/dex-retargeting
3. https://github.com/vuer-ai/vuer
4. https://github.com/stack-of-tasks/pinocchio
5. https://github.com/casadi/casadi
6. https://github.com/meshcat-dev/meshcat-python
7. https://github.com/zeromq/pyzmq
8. https://github.com/Dingry/BunnyVisionPro
9. https://github.com/unitreerobotics/unitree_sdk2_python
10. https://github.com/ARCLab-MIT/beavr-bot

# 7. 📝 Citation

```
@misc{xr-teleoperate,
  author       = {{Unitree Robotics}},
  title        = {{XR-Teleoperate}: An Open-Source Teleoperation Framework and Data Collection Toolkit for Embodied Intelligence},
  howpublished = {\url{https://github.com/unitreerobotics/xr_teleoperate}},
  year         = {2024},
  note         = {Accessed: 2026-02}
}
```
