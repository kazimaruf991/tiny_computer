# 小小电脑

<img decoding="async" src="readme/cover0.png" width="50%">

给所有安卓arm64设备的“PC应用引擎”平替

Click-to-run debian bookworm xfce on android for Chinese users, with fcitx pinyin input method preinstalled. No termux required.

## 特点

- 一键安装，即开即用
- 来自kali-undercover的win10主题(仅xfce版本)，友好的界面

<img decoding="async" src="readme/img1.png" width="50%">

- 提供常用软件的一键安装指令

<img decoding="async" src="readme/img2.png" width="50%">

- 可方便地改变屏幕缩放，不用担心屏幕过大或过小

<img decoding="async" src="readme/img3.gif" width="50%">

- 便捷访问设备文件，或通过设备SAF访问软件文件

<img decoding="async" src="readme/img4.png" width="50%">

- 提供终端和众多可调节参数供高级用户使用

<img decoding="async" src="readme/img5.png" width="50%">

## 原理

使用proot运行debian环境

内置[noVNC](https://github.com/novnc/noVNC)显示图形界面

## 项目结构

assets的文件来源信息可以在[这里](extra/readme.md)找到。

完整的容器制作过程可以在[这里](extra/build-tiny-rootfs.md)看到。

数据包不再在assets中更新，而是随releases提供，主要是为了避免git越来越大

lib目录：

- main.dart文件，页面布局，有点乱
- workflow.dart文件，逻辑部分，目前也还可以理解
  - Util 工具类
  - TermPty 一个终端
  - G 全局变量类
  - Workflow 从软件点开到容器启动的所有步骤

## 编译

你需要配置好flutter和安卓sdk，然后克隆此项目。

在编译之前，需要在release中下载系统rootfs(或者[自行制作](extra/build-tiny-rootfs.md))，之后使用split命令分割，拷贝到assets。一般我将其分为98MB。

`split -b 98M debian.tar.xz`

接下来就可以编译了。我使用的命令如下：

`flutter build apk --target-platform android-arm64 --split-per-abi --obfuscate  --split-debug-info=tiny_computer/sdi`

## 目前已知bug

多用户/分身情形无法sudo, 其它见issue

## 一些链接

这是我的第一个flutter软件，感谢这些项目为我指路

- 要一点基础的 [《Flutter实战·第二版》](https://book.flutterchina.club)
- 也许是零基础的Flutter视频课程 [freeCodeCamp Flutter Course](https://www.youtube.com/watch?v=wFn-m-OgKPU&list=PL6yRaaP0WPkVtoeNIGqILtRAgd3h2CNpT)

- 安卓上的VS Code [Code FA](https://github.com/nightmare-space/vscode_for_android)

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.
