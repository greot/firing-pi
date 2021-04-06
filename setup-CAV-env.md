# computer audio & video dev env

[我是工程师, 不是程序员. 我的工作不是写代码, 而是合理地使用工具解决问题](https://www.leiphone.com/news/201703/2MCSRGD5XpPNbK8c.html)

- 开启摄像头:
  + `raspi-config` -> `Interface Options` -> `Camera`
  + `sudo apt-get install luvcview` [查看摄像头的实时视频](https://blog.csdn.net/weixin_45880057/article/details/113965373)
  + `luvcview -s 1080x720` 设置采集分辨率

- [第一个安装OpenCV的参考](原文链接：https://blog.csdn.net/q759451733/article/details/104082589)
	1. 更新和升级现有软件包
		  + sudo apt-get update && sudo apt-get upgrade
	2. 我们需要安装一些开发人员工具，包括CMake，它可以帮助我们配置OpenCV构建过程
		  + sudo apt-get install build-essential cmake pkg-config
	3. 安装映像I/O包，以允许我们从磁盘加载各种映像文件格式。此类文件格式的示例包括JPEG，PNG，TIFF等
		  + sudo apt-get install libjpeg-dev libtiff5-dev libjasper-dev libpng-dev
	4. 安装视频I/O包。这些库使我们可以从磁盘读取各种视频文件格式，以及直接使用视频流
		  + sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
		  + sudo apt-get install libxvidcore-dev libx264-dev
	5. OpenCV库带有一个名为highgui的子模块，该子模块 用于在我们的屏幕上显示图像并构建基本的GUI。为了编译 highgui模块，我们需要安装GTK开发库和前提条件
		  + sudo apt-get install libfontconfig1-dev libcairo2-dev
		  + sudo apt-get install libgdk-pixbuf2.0-dev libpango1.0-dev
		  + sudo apt-get install libgtk2.0-dev libgtk-3-dev
	6. 安装一些额外的依赖项，可以进一步优化OpenCV内部的许多操作
		  + sudo apt-get install libatlas-base-dev gfortran
	7. 用于HDF5数据集和Qt GUI
		  + sudo apt-get install libhdf5-dev libhdf5-serial-dev libhdf5-103
		  + sudo apt-get install libqtgui4 libqtwebkit4 libqt4-test python3-pyqt5
	8. 如果您的RPi上装有Raspberry Pi摄像机模块，则还应该安装  PiCamera API
		  + pip install "picamera[array]"
	9. 安装OpenCV
		  + pip install opencv-contrib-python==4.1.0.25 # '=='后面是版本号
	10. 测试OpenCV是否安装成功
	```
		python3
		>>> import cv2
		>>> cv2.__version__
        '4.1.0'
   ```
   
- [另一个安装OpenCV的参考](https://blog.csdn.net/x115104/article/details/78878599)
  + `sudo apt-get update` 保证各个软件都是最新的，你将要下载很多东西，请保证网络畅通。
  + `sudo apt-get install build-essential` 安装编译OpenCV必不可少的依赖库
  + `sudo apt-get install build-libavformat-dev` 该库提供一种音视频码流的编解码方法
  + `sudo apt-get install python-opencv` OpenCV所依赖的Python开发包
  + `sudo apt-get install opencv-doc` # 安装OpenCV开发文档，万一你需要呢
  + `sudo apt-get install ffmpeg` 该库提供音视频流的转码功能
  + `sudo apt-get install libcv-dev` 安装编译OpenCV所需要的头文件和静态库
  + `sudo apt-get install libcvaux-dev` 安装更多的开发工具来编译OpenCV
  + `sudo apt-get install libhighgui-dev` 安装另一个编译OpenCV所需要的头文件和静态库
  + `cp -r /usr/share/doc/opencv-doc/examples /home/pi/` 将所有示例拷贝到你的根目录

- [编译安装OpenCV的备用参考](http://www.nrjs.cn/ctt/11120036.html); **也可以参考使用OpenMV库**

- 安装iPython
```
cd /home/pi/miniconda3/bin
conda install ipython
```
