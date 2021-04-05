# 烧录树莓派 

- Raspberry Pi 4B, [树莓派官网](https://www.raspberrypi.org/)
- 无屏幕, VNC
- auto WIFI, SSH
- DEBIAN LINUX, XFCE4
- `Micro SD卡`(32G+), `读卡器`

## 1 烧镜像
- 从[官网软件栏](https://www.raspberrypi.org/software/)下载烧录器(Raspberry Pi Imager); 或者自行下载安装非官方, 但同样好用的 balena-etcher.
- 从[官网操作系统栏](https://www.raspberrypi.org/software/operating-systems/)下载系统镜像(Raspberry Pi OS with desktop [and recommended software]).
- 自行准备`Micro SD卡`(32G+), 利用`烧录器`, 从个人主机上将`系统镜像`写入`Micro SD卡`中(通常需要通过`读卡器`进行; 烧录时无需解压系统镜像).

## 2 配`boot`
在烧录好的SD卡中, 找到`\boot`卷, 
- 创建名为`ssh`的空文件, 表示允许SSH接入
- 创建名为`wpa_supplicant.conf`的文件, 内容如下:
```
country=CN
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
# ap_scan=2 # 1: 优先连接可见WIFI; 2: 按优先级先后次序连接

network={
    ssid="WiFi-A"   # 自己的WIFI名称
    psk="12345678"  # 自己的WIFI密码
    key_mgmt=WPA-PSK
    priority=9  # 数字越大, 优先级越高
}

network={
    ssid="WiFi-B"
    psk="12345678"
    key_mgmt=WPA-PSK
    priority=3
}

network={
    ssid="WiFi-C"
    psk="12345678"
    key_mgmt=WPA-PSK
    priority=1
}
```

## 3 初体验
- 将SD卡装入树莓派, 连接适配器(USB-C电源 5V 3A)
- 待树莓派启动后(红灯常亮, 绿灯偶闪), 从网络管理界面(如tplogin.cn), 或使用`arp`等命令, 找到树莓派的IP地址(eg, 192.168.0.99)
- 用SSH连接树莓派: ssh pi@192.168.0.99 (登录密码为raspberry)
- 在树莓派上运行`sudo raspi-config`, 
  + 通过`interface Options` -> `VNC`, 启动VNC
  + 可以修改掉`pi`用户的密码
  + 通过`Advanced Options` -> `Resolution`, 调节分辨率(*系统将重启*)

## 4 入佳境
- 重启树莓派后, 使用VNC viewer连接之
- 按照屏幕提示进行配置
- 安装neovim, fish, awesomeWM, tmux, mpv, gdebi, fortune, git, build-essential, cmake, go, rustc, cargo等常用工具 (不需手动換源)
- 安装MiniConda, 好玩Python
```
wget http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-armv7l.sh
sudo /bin/bash Miniconda3-latest-Linux-armv7l.sh # -> change default directory to /home/pi/miniconda3
```
- 配置`~/.bashrc`, 自动启动fish, 设置fish和nvim的别名等, 并`export PATH="/home/pi/miniconda3/bin:$PATH"`
