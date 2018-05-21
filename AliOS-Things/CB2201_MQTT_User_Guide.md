# 手把手教你在CB2201开发板上使用MQTT通道上云

本文基于 [AliOS Things](https://github.com/alibaba/AliOS-Things) 1.3.x版本，手把手教你如何在CB2201上使用mqtt上云

## **1 硬件环境搭建**

### 1.1 开发板准备

#### 1.1.1 CB2201 YMC2HQFNR1A（赤焰剑）开发板介绍

**①** 赤焰剑开发板是杭州中天微全自主设计一款用于开发IoT 应用的开发板。板上集成中天微设计的基于中天微CK802 CPU核的CH2201芯片；集成了CPU调试器CKLink，只需要一根USB线就可以供电、调试、下载等操作。

**②** CH2201芯片内部集成C-SKY CK802 CPU核，集成AES,SHA,CRC,TRNG等安全相关模块。

**③** 超低功耗设计，低功耗模式下，CH2201芯片核心电流小于3uA，QFP-64-0.4mm封装。

**④** 集成两个外设接口，每个外设接口中都集成了UART/SPI/IIC/ADC/PWM/GPIO等接口，可以连接各类接口兼容的功能子板，包括中天微设计的ENC28J60 SPI有线网卡子板，ESP8266-WiFi子板，传感器子板等。

![CB2201](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/CB2201.png)

#### 1.1.2 ESP8266 WiFi子板

WiFi子板介绍：略

![ESP8266_evb](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/ESP8266_evb.png)

### 1.2 开发板连接方法

1、WiFi子板连接

![CB2201_ESP8266_evb](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/CB2201_ESP8266_evb.png)

2、串口线连接

![USB_Serial](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/USB_Serial.png)

3、电源连接

通过USB线供电，图略

## 2 云端和通道环境搭建

### 2.1 在云端主要包括以下几步

参考链接（https://github.com/alibaba/AliOS-Things/wiki/Manual-Channel-MQTT），做如下操作：

1、创建阿里云账号

2、创建测试产品，拿到ProductKey

3、创建测试设备，拿到DeviceName和DeviceSecret

4、下载测试工具

注意：请无视该文档中关于linuxhost的示例，编译方式请参考下面章节。

### 2.2 三要素设置

修改./framework/protocol/linkkit/iotkit/sdk-encap/imports/iot\_import\_product.h 三个宏定义，修改为上一步骤中创建产品和设备时拿到的三要素（ProductKey、DeviceName和DeviceSecret），如下：

```

#elif  MQTT\_TEST

#define PRODUCT\_KEY    "......"

#define DEVICE\_NAME    "......"

#define DEVICE\_SECRET  "......"

#define PRODUCT\_SECRET ""

#else

```

注：mqttapp程序所在源码为AliOS-Things/example/mqttapp/mqtt-example.c (https://github.com/alibaba/AliOS-Things/blob/master/example/mqttapp/mqtt-example.c)。

此时在云端获取的三个参数ProductKey，DeviceName和DeviceSecret分别对应代码中的PRODUCT\_KEY，DEVICE\_NAME和DEVICE\_SECRET三个宏。

## 3 mqttapp编译

AliOS-Things支持开发方式：命令行和AliOS-Things IDE，详见下面说明。

### 3.1 命令行编译

1、命令行环境搭建：

参考https://github.com/alibaba/AliOS-Things/wiki/Quick-Start

2、命令行编译方式如下：

`$ aos make mqttapp@cb2201`

build完成后可在out/mqttapp@cb2201/binary/ 目录找到生成的bin文件和hex文件。

### 3.2 AliOS-Things IDE编译

1、AliOS-Things IDE环境搭建：

  参考https://github.com/alibaba/AliOS-Things/wiki/Starter-Kit-Tutorial

2、开发环境搭建好后，导入Alios-Things源码
3、Build如下图，选中mqttapp@cb2201，点击右侧&quot;√&quot;


build完成后可在out/mqttapp@cb2201/binary/ 目录找到生成的bin文件。

## 4 固件烧录

### 4.1 安装烧录软件

1、烧录软件获取：链接：https://pan.baidu.com/s/1fWUThsODomSQIj99Ja1Bag 密码：wkbb

2、解压后，双击CSKYFlashProgrammer.exe打开烧录软件

### 4.2 烧录

1、选择User Config： AliOS-Things-CB2201-MQTTAPP，更改AliOS-Things存放路径（即修改下图中“G:\”）

2、点击下方"Start Program"按钮烧写

![FLASH_PROGRAMMER_Config](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/FLASH_PROGRAMMER_Config.png)

## 5 WiFi配网及数据连接阿里云

### 5.1 WiFi配网

烧录完成后，点击复位键启动串口打印如下图所示：

在串口命令行中敲入如下配网命令：

`# netmgr connect <ssid> <password>`

![PeiWang](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/PeiWang.png)

正常联网后，mqttapp会真正开始运行。下图为mqttapp运行日志截图：

![mqttapp_log](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/mqttapp_log.png)

### 5.2 查看设备是否在线

点击下面链接，登录阿里云账户查看：

[http://iot.console.aliyun.com/#/product/newlist/region/cn-shanghai](http://iot.console.aliyun.com/#/product/newlist/region/cn-shanghai)

## 6 调试

### 6.1 CskyDebugServer安装和使用

1、获取CskyDebugServer（若已安装CDS/CDK，则可略过1和2的步骤）

链接：https://pan.baidu.com/s/1aXN3wIysVVthEN4QaPvRww 密码：ecs9

2、安装

  解压后双击默认安装

3、端口设置，如下图：

![CskyDebugserver_port](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/CskyDebugServer_port.png)

4、连接开发板

点击 “红色三角形” 按钮，连接成功后，“红色三角形” 按钮会变成 “红色圆形” 按钮，如下图：

![CskyDebugServer_connect](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/CskyDebugServer_connect.png)

### 6.2 VS Code调试设置

根据已编译并烧录的app@board信息，更新 AliOS-Things/.vscode/launch.json 调试配置文件，比如：已编译并烧录 mqttapp@cb2201以后，更改相关配置：

![VSCode_launch](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/VSCode_launch.png)

### 6.3 开始调试

1、点击 ![VSCode_Debug_Page_Button](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/VSCode_Debug_Page_Button.png) 按钮，进入调试界面

2、选择CSKY DEBUG：![VSCode_CSKYDebug_Button](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/VSCode_CSKYDebug_Button.png)

3、点击左上方的 ![VSCode_Continue](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/VSCode_Continue.png) 按钮(或F5)启动调试

4、启动调试以后会自动转到已设置的断点 application\_start 函数处，同时上方会出现调试工具栏，提供常用的单步调试功能

![VSCode_debug](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/AliOS-Things/VSCode_debug.png)

