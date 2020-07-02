# 通过TNN架构将模型部署至移动端

参考项目：https://github.com/Laugigabyte/TNN

步骤：
  + 将模型转换成ONNX模型。（此处以pytorch模型为例）
  + 将ONNX模型转换成TNN模型部署至移动端。

首先：
```
git clone https://github.com/Laugigabyte/TNN.git
```
# Demo 代码介绍

## 一、iOS Demo 介绍

### Demo运行步骤

1. 下载Demo模型

   ```
   cd <path_to_tnn>/model
   sh download_model.sh
   ```

2. 打开TNNExamples工程

   进入目录`<path_to_tnn>/examples/ios/`，双击打开TNNExamples工程。

3. 设置开发者账号

   如下图点击TNNExamples工程，找到工程设置`Signing & Capabilities`，点击Team选项卡选择`Add an Account...`

   ![NTuCPs.jpg](https://s1.ax1x.com/2020/07/01/NTuCPs.jpg)

   在如下界面输入Apple ID账号和密码，添加完成后回到`Signing & Capabilities`界面，并在Team选项卡中选中添加的账号。如果没有Apple ID也可以通过`Create Apple ID`选项根据相关提示进行申请。

   ![NTuAMV.jpg](https://s1.ax1x.com/2020/07/01/NTuAMV.jpg)

   **此处注意证书问题：`Signing Certificate`应确保有证书，否则将无法在真机上测试；如有团队则可进入团队共享团队的证书资源。**

4. 真机运行  

   4.1 修改`Bundle Identitifier`

   如图在现有`Bundle Identifier`后随机添加后缀（限数字和字母），避免个人账户遇到签名冲突。

   [![NTKFFH.jpg](https://s1.ax1x.com/2020/07/01/NTKFFH.jpg)](https://imgchr.com/i/NTKFFH)

4.2 验证授权
   
首次运行先利用快捷键`Command + Shift + K`对工程进行清理，再执行快捷键`Command + R`运行。如果是首次登陆Apple ID，Xcode会弹框报如下错误，需要在iOS设备上根据提示进行授权验证。一般来说手机上的授权路径为：设置 -> 通用 -> 描述文件与设备管理 -> Apple Development选项 -> 点击信任

![NTKAfA.jpg](https://s1.ax1x.com/2020/07/01/NTKAfA.jpg)
4.3 运行结果
   
首次运行先利用快捷键`Command + Shift + K`对工程进行清理，再执行快捷键`Command + R`运行。默认界面为人脸检测，可以点击右上角编辑按钮切换图像分类等不同功能。
   
PS：
   
a) 由于GPU和CPU加速原理不同，具体模型的GPU性能不一定比CPU高，与具体机型、模型结构以及工程实现有关。欢迎大家参与到TNN开发中，共同进步。
   
b) TNNSDKSample.h中的宏TNN_SDK_USE_NCNN_MODEL默认为0，运行TNN模型，可以设置为1来运行ncnn模型。
   
   c) 如遇到`Unable to install...`错误提示，请在真机设备上删除已有的TNNExamples，重新运行安装。
   
   d) 真机运行时，如果遇到CodeSign错误`Command CodeSign failed with a nonzero exit code`，可参看issue20 `iOS Demo运行步骤说明`

### Demo运行效果

1. 人脸检测

   模型来源：https://github.com/Linzaer/Ultra-Light-Fast-Generic-Face-Detector-1MB

   效果示例：iPhone 11 pro max, ARM GPU 5.9066ms

  ![NTKUmT.png](https://s1.ax1x.com/2020/07/01/NTKUmT.png)

2. 图像分类

   模型来源：https://github.com/forresti/SqueezeNet

   效果示例：iPhone 11 pro max, ARM GPU 8.18ms

  ![NTKy11.png](https://s1.ax1x.com/2020/07/01/NTKy11.png)

## 二、Android Demo 介绍

### 运行环境要求

1. Android Studio 3.5 或以上
2. NDK version >= 16

### 运行环境

1. Android Studio 4.0
2. NDK(`Android Studio/Preference`中找到Android SDK，并选择SDK Tools下载相对版本的NDK和CMake点击Aplly后下载安装，否则将报错；再次提醒，版本问题很重要)

![NTMZ4J.png](https://s1.ax1x.com/2020/07/01/NTMZ4J.png)

[![NTM9cq.md.png](https://s1.ax1x.com/2020/07/01/NTM9cq.md.png)](https://imgchr.com/i/NTM9cq)

### 运行步骤

1. 下载Demo模型

   ```
   cd <path_to_tnn>/model
   sh download_model.sh
   ```


2. 打开TNNExamples工程

   打开`Android Studio`，点击`Open an existing Android Studio project`，选择目录`<path_to_tnn>/examples/android/`，双击打开TNNExamples工程。

   ![NTMtCd.png](https://s1.ax1x.com/2020/07/01/NTMtCd.png)

### 运行效果
1. 人脸检测-图片
   
   模型来源：https://github.com/Linzaer/Ultra-Light-Fast-Generic-Face-Detector-1MB

   效果示例：realme X50, ARM GPU 13.953ms

   ![NT8SOI.jpg](https://s1.ax1x.com/2020/07/01/NT8SOI.jpg)


2. 图像分类

   模型来源：https://github.com/forresti/SqueezeNet

   效果示例：realme X50, ARM GPU 12.6933ms

   ![NT8ktS.jpg](https://s1.ax1x.com/2020/07/01/NT8ktS.jpg)


## 总结
  + IOS端注意证书问题。
  + Android端注意版本对应问题。
