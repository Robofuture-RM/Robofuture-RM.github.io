---
title: STM32CubeIDE使用笔记 01：基础使用与说明
tags: STM32CubeIDE STM32
author: Zhb-Wave
show_author_profile: true
modify_date: 2021-02-04
---

## 目的

STM32cubeIDE是ST官方推出的一款用于开发STM32的工具，在这里进行记录软件安装过程，并对界面进行说明。

<!--more-->

## 安装

软件可以在ST官网获取：[传送门](https://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-ides/stm32cubeide.html)。安装一直下一步即可完成安装：

![install-01](http://robofuture.net.cn/assets/images/STM32CubeIDE/install-01.png)

![install-02](http://robofuture.net.cn/assets/images/STM32CubeIDE/install-02.png)

![install-03](http://robofuture.net.cn/assets/images/STM32CubeIDE/install-03.png)

![install-04](http://robofuture.net.cn/assets/images/STM32CubeIDE/install-04.png)

![install-05](http://robofuture.net.cn/assets/images/STM32CubeIDE/install-05.png)

![install-06](http://robofuture.net.cn/assets/images/STM32CubeIDE/install-06.png)

## 软件的使用与界面说明

### 1.选择工作空间

打开软件后，先会让我们选择工作空间。那么这个工作空间的作用是什么呢：

- 相关项目的集合，可以把相关的项目放在同一个工作空间中（与VS中类似）；
- 需要同样配置（项目配置）的一组项目集合（这点与VS不太一样，VS里面设置了之后是对每个解决方案都一样的）；
- 需要同样Eclipse设置（IDE本身的设置，例如快捷键等）的一组项目集合。

选择好工作空间后就可以使用IDE了。

![select_workspace](http://robofuture.net.cn/assets/images/STM32CubeIDE/select_workspace.png)

### 2.新建项目

下面我们需要开始一个新项目，选择 `Start new STM32 project`。

![start_porject](http://robofuture.net.cn/assets/images/STM32CubeIDE/start_porject.png)

### 3.选择芯片

选择开发板使用的芯片

![MCU_selection](http://robofuture.net.cn/assets/images/STM32CubeIDE/MCU_selection.png)

### 4.基础设置

这里只需设置项目名字（Project Name），其他都保持默认

![porject_setup](http://robofuture.net.cn/assets/images/STM32CubeIDE/porject_setup.png)

![firmware_setup](http://robofuture.net.cn/assets/images/STM32CubeIDE/firmware_setup.png)

### 5.引脚设置

在这里根据我们的项目和 PCB 进行引脚的设置，设置完后生成代码

![mx_configuration](http://robofuture.net.cn/assets/images/STM32CubeIDE/mx_configuration.png)

### 6.编辑代码

下面我们进行代码的编写，编写功能代码后，需要先进行编译，然后才可以进行调试

![edit_code](http://robofuture.net.cn/assets/images/STM32CubeIDE/edit_code.png)

### 7.调试与运行

在进行调试前，还需要进行配置，点击调试按钮![debug_button](http://robofuture.net.cn/assets/images/STM32CubeIDE/debug_button.png)，进入Debug Configuration，选择使用的调试器，配置完成后就能进行调试

![debug_config](http://robofuture.net.cn/assets/images/STM32CubeIDE/debug_config.png)

![debug](http://robofuture.net.cn/assets/images/STM32CubeIDE/debug.png)

## 常用快捷键

STM32CubeIDE快捷键很多，可以通过 `Help > Show Active Keybindings...` 查看当前可用快捷键；也可以在 `Window > Preferences > General > Keys` 中查看修改快捷键，默认的常用快捷键如下（一些特别常用的就不写了）：

| 快捷键       | 快捷键说明               |
| ------------ | ------------------------ |
| Ctrl+/       | 注释行/取消注释行        |
| Ctrl+D       | 删除行                   |
| Ctrl+Shift+F | 格式化代码               |
| Alt+/        | 代码补全                 |
| Shift+Enter  | 在当前行的下一行插入空行 |
| Alt+↓/↑      | 行下移/上移              |
| Ctrl+↑/↓     | 编辑器视图上移/下移      |
| Alt+←/→      | 前一个/后一个页面        |
| F3           | 跳转到声明处             |
| Ctrl+F       | 文件内内搜索             |
| Ctrl+H       | 项目内搜索               |
| Ctrl+M       | 最大化/默认当前窗口      |
| Ctrl+L       | 跳转至某行               |
| Ctrl+O       | 显示大纲（方便跳转）     |
| Ctrl+W       | 关闭当前窗口             |
| F11          | 启动调试                 |
| F5           | 单步跳入（调试时）       |
| F6           | 单步跳过（调试时）       |
| F7           | 单步返回（调试时）       |
| F8           | 继续运行（调试时）       |

## 文件夹说明

![file_specification](http://robofuture.net.cn/assets/images/STM32CubeIDE/file_specification.png)

## 其他配置

### 1 在高分辨率下工具栏图标太小

我们选择要启动的软件，鼠标右键，打开属性，选择兼容性->更改高 DPI 设置：

![DPI_config-01](http://robofuture.net.cn/assets/images/STM32CubeIDE/DPI_config-01.png)

![DPI_config-02](http://robofuture.net.cn/assets/images/STM32CubeIDE/DPI_config-02.png)

勾选`替代高 DIP 缩放行为`，在下面的选择框中选择`系统（增强）`

![DPI_config-03](http://robofuture.net.cn/assets/images/STM32CubeIDE/DPI_config-03.png)