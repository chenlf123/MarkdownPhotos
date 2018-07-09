# Arduino体验

本文介绍从零开始体验Arduino开发板

# 1 购买Arduino开发板

从淘宝七星虫旗舰店，618活动价172元（原价238元）购买了一整套开发板套件，包含如下：

1. Arduino开发板1块
2. 入门书：《Arduino入门到实践》
3. 透明双卡扣收纳盒
4. 专业实验套件DVD资料盘
5. 其它小器件包含：面包板1块、USB线、马达2种、大/小数码管、风扇叶、发光二极管、数字按键、红外遥控器、液晶屏、电阻电容、杜邦线等。

淘宝链接：[https://detail.tmall.com/item.htm?id=35121893747&spm=a1z09.2.0.0.1bcb2e8dC5Sumu&_u=7at3rl743ec](https://detail.tmall.com/item.htm?id=35121893747&spm=a1z09.2.0.0.1bcb2e8dC5Sumu&_u=7at3rl743ec)

# 2 开发环境

## 2.2 下载IDE

从Arduino官网下载IDE arduino-1.8.5-windows.exe，共90.4MB大小，下载速度很快，下载时无需登录。

链接：[https://www.arduino.cc/en/Main/Donate](https://www.arduino.cc/en/Main/Donate)

## 2.3 安装IDE

安装文件只有1个EXE文件，无需解压，双击打开安装，非常方便。如下图：

![Arduino_IDE_Install_1](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_Install_1.png)

![Arduino_IDE_Install_2](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_Install_2.png)

## 2.4 初识IDE

### 2.4.1 打开进入IDE

安装完后，会在桌面生成一个快捷方式，双击打开，如下图加载界面：

![Arduino_IDE_1](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_1.png)

进入IDE后，发现支持中文，惊喜！

![Arduino_IDE_2](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_2.png)

### 2.4.2 按钮介绍

下图 “验证” 按钮：编译验证程序。

![Arduino_IDE_Button_1](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_Button_1.png)

下图 “上传” 按钮：编译并下载程序到开发板。

![Arduino_IDE_Button_2](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_Button_2.png)

下图 “新建” 按钮：点击会新生成一个窗口。

![Arduino_IDE_Button_3](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_Button_3.png)

下图 “打开” 按钮：可以打开OS文件系统内的工程，也可打开IDE提供的Demo工程

![Arduino_IDE_Button_4](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_Button_4.png)

下图 “保存” 按钮：保存工程

![Arduino_IDE_Button_5](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_Button_5.png)

# 3 正式使用

## 3.1 编译测试
编译时间：简单工程大概是2秒钟时间

编译输出信息：如下图，有简单粗的提示信息。

![Arduino_IDE_Build](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_Build.png)

编译出错时的信息：可以复制错误信息（右侧按钮，这个功能不错），如下图：

![Arduino_IDE_Build_Error](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_Build_Error.png)

## 3.2 固化程序

1. 先用USB线把开发板和电脑连接起来；
2. 再打开IDE，打开后会自动连接上开发板，如下图；
3. 点击“上传”按钮下载程序。
![Arduino_IDE_COM](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_COM.png)

## 3.3 编写LED测试程序

按照《Arduino入门到实践》书中描述的digital接口，写了个跑马灯程序，比较顺利，实景图：

![Arduino_LED_Practce](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_LED_Practce.jpg)


玩的过程中，跳出个小窗口说有更新，没及时点进去消失了，遗憾。

![Arduino_IDE_Update](https://raw.githubusercontent.com/chenlf123/MarkdownPhotos/master/Arduino/Arduino_IDE_Update.png)

# 4 体验感受

## 4.1 开发板

优点：

1. 开发板套件的电子元器件配套全，各种实验器件都可以找到，并且对应实验器材的使用有对应小视频介绍。
2. 开发板体积小，提供USB供电和DC-5.5*2.1接口供电
3. 开发板上的数字标志明确
4. 整体包装精美

缺点：

1. 开发板没有固定脚。自己找了几个脚接上去，发现瘸脚，一个螺丝脚接不上去，原因是位置太挤而螺帽太大
2. GPIO口相对较少
3. 开发板的UART、SPI、IIC等接口没有标志
4. 暂时没找到芯片和开发板的总体资源介绍

## 4.2 开发使用

优点：

1. IDE安装包小，下载方便快捷，只有1个EXE，比较清爽干净
2. IDE支持多种操作系统：Windows XP/7/8/10、Mac OS X、Linux32/64、Linux ARM
3. IDE按钮少、轻巧，乍一看是一个文本编辑器；然而菜单栏的隐藏功能却不少
4. IDE支持中文
5. IDE打开就直接连接上开发板
6. IDE编译和下载速度快
7. IDE提供较多的Demo程序。
8. 提供20多个库支持包括，括Robots、Ethernet、SD、SPI、Wi-Fi、键鼠、GSM等
9. 驱动接口：进行了接口的封装，使得用起来简单
10. 视频教程、书本信息齐全
11. 总体上手非常快

缺点：

1. 有时会出现插拔USB线导致和IDE连接不上的问题
2. 没看到深度开发的方法，看不到底层函数的实现
3. 总体上说，仅适合面向应用开发的人员

## 4.3 总结

总的来说，买到的Arduino开发板是很不错的开发板，使用简单，定位明确，适合教学、实验等小应用开发。开发板资料比较多，由于时间问题，没有看完。相信Arduino还有更多针对专业领域的开发板，期待体验！