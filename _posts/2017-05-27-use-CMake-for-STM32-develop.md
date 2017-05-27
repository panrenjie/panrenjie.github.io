---
layout:     post
title:      "Ubuntu下使用CMake搭建STM32开发环境"
subtitle:   "Linux下开发stm32"
date:       2017-05-27
author:     "Jecy"
header-img: "img/post-build-a-blog.jpg"
tags:       
    -   STM32
    -   CMake
    -   FreeRTOS
    -   开发环境
---




### 摘要

本文介绍在Ubuntu环境下，如何搭建STM32（以STM32F407为例）开发环境。     
软件版本如下：    
> Ubuntu: 14.04         
arm-none-eabi:5.4.1         
Cmake:3.8.1         
OpenOCD: 0.10.0     
STM32CubeMX: 4.21.0
Java: 1.8.0_131
硬件平台：正点原子的探索者开发板。
IC型号STM32F407ZGT6



以下是开发过程中需要使用的软件以及安装方法，方法针对Ubuntu新手,老司机可略过。

### Cmake安装
1、下载cmake安装文件。  [下载地址](https://cmake.org/download/)
选择cmake-3.8.1-Linux-x86_64.tar.gz，保存到本地。
2、将安装包移动到/usr/local/目录下，并解压。
`mv cmake-3.8.1-Linux-x86_64.tar.gz /usr/local
tar -xvf cmake-3.8.1-Linux-x86_64.tar.gz`
3、打开`/etc/profile`文件,在文件最后添加
`export PATH=/usr/local/cmake-3.8.1-Linux-x86_64/bin:$PATH`
4、使环境变量生效。`source /etc/profile`
5、终端输入 `cmake -version`,打印 cmake version 3.8.1，安装成功。

### Jlink安装
1、下载JLink安装包。 [下载地址]( https://www.segger.com/downloads/jlink)
找到 J-Link Software and Documentation pack for Linux, DEB Installer, 64-bit。（如果系统是32位，请选择32-bit），下载之后，直接双击安装。

### GCC工具链安装
1、下载GCC工具链安装包。[下载地址](https://launchpad.net/gcc-arm-embedded/+download)
选择gcc-arm-none-eabi-5_4-2016q3-20160926-linux.tar.bz2，保存的本地。
2、将安装包移动到/usr/bin/目录下，并解压。
`mv gcc-arm-none-eabi-5_4-2016q3-20160926-linux.tar.bz2 /usr/bin
    tar -jxvf gcc-arm-none-eabi-5_4-2016q3-20160926-linux.tar.bz2`
3、添加环境变量。
打开`/etc/profile`文件,在文件最后添加
`export PATH=/usr/bin/gcc-arm-none-eabi-5_4-2016q3/bin:$PATH`
4、使环境变量生效。`source /etc/profile`
5、终端输入 `arm-none-eabi-gcv -v`,打印 gcc version 5.4.1，安装成功。

### openocd安装
1、下载源码。

```
git clone git://git.code.sf.NET/p/openocd/code openocd           
cd openocd                
./bootstrap                  
./configure –enable-maintainer-mode –enable-usb_blaster_libftdi                    
make            
sudo make install                       
openocdopen -v
```
安装时候，可能还需要安装其他软件，否则报错。      
`sudo apt-get install libtool`      
`sudo apt-get install libftdi*`     
`sudo apt-get install libusb-1.0.0-dev`         

到这里，开发环境就搭建好了。
### 工程编译
已经配置好的工程模版已经上传到了github上。
地址：git@github.com:panrenjie/STM32F4_FreeRTOS_Blinky.git
代码下载到本地后，按照下面的步骤，进行编译。

`cd STM32F4_FreeRTOS_Blinky.git
cd Build
cmake ..
make `
编译好后，hex文件会存放在Build/bin目录下。

>整套代码的编译是通过CMAKE来进行的。如果你想在此模版的基础上开发项目，则需要了解cmake的使用方法，需要对相应文件夹下的CMakeLists.txt文件进行修改。cmake的使用方法不在本文展开。

### 代码烧写

1、打开终端，输入
`openocd -f interface/jlink.cfg -f target/stm32f4x.cfg`
2、重新打开另外一个终端，输入
`telnet localhost 4444
halt
flash write_image erase /home/111/STM32F4_FreeRSOS_Blinky/Build/bin/blinky.hex
reset`
这时候，会看到板子上LED灯开始闪烁。至此，就完成了Ubuntu下stm32代码的编译、烧写过程。
最后，可以输入`shutdowm`退出。







