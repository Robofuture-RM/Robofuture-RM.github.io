---
title: STM32CubeIDE使用笔记 02：STM32CubeMX简单使用
tags: STM32CubeIDE STM32 STM32CubeMX
author: Zhb-Wave
show_author_profile: true
modify_date: 2021-02-10
---

## 目的

STM32cubeIDE 中带有 STM32CubeMX 来进行芯片引脚功能的配置，在这里我们将学习了解配置界面，并进行简单的配置。

<!--more-->

## 界面介绍

STM32CubeMX 主要由四部分组成引脚配置、时钟配置、项目管理、工具。下面对每个页面进行具体说明。

### 引脚配置

这个页面可以配置引脚、外设和第三方库，需要根据具体情况进行配置：

![pinout_configuration](http://robofuture.net.cn/assets/images/STM32CubeIDE/pinout_configuration.png)

### 时钟配置

这个页面主要配置系统时钟：

![clock_configuration](http://robofuture.net.cn/assets/images/STM32CubeIDE/clock_configuration.png)

#### STM32中的几个时钟SysTick、FCLK、SYSCLK、HCLK

在STM32中，有五个时钟源，为HSI、HSE、LSI、LSE、PLL。

1. HSI是高速内部时钟，RC振荡器。
2. HSE是高速外部时钟，可接石英/陶瓷谐振器，或者接外部时钟源。
3. LSI是低速内部时钟，RC振荡器。
4. LSE是低速外部时钟，接频率为32.768kHz的石英晶体。
5. PLL为锁相环倍频输出。

其中**LSI(低速内部时钟)**和**LSE(低速外部时钟)**可以选择为**RTC(实时时钟)**时钟源

**SYSCLK**：系统时钟，它是供STM32中绝大部分部件工作的时钟源。系统时钟可由PLL、HSI或者HSE提供输出，并且它通过AHB分频器分频后送给各模块使用，其中AHB分频器输出的时钟到5大模块使用： 

1. 输出到AHB总线、内核、内存和DMA使用的HCLK时钟。
2. 分频后输出给STM32芯片的系统定时器时钟。
3. 直接输出给Cortex的自由运行时钟FCLK(free running clock，在处理器休眠时，通过FCLK 保证可以采样到中断和跟踪休眠事件)。
4. 输出到APB1分频器。其输出一路供APB1外设使用(PCLK1)，另一路送给定时器(Timer)使用。
5. 输出到APB2分频器。其输出一路供APB2外设使用(PCLK2)，另一路送给定时器(Timer)使用。

**FCLK**：CPU内核的时钟信号，我们所说的cpu主频为XXXXMHz，就是指的这个时钟信号，相应的，1/FCLK即为cpu时钟周期。

**HCLK**：AHB总线时钟，由 SYSCLK 分频得到，一般不分频，等于系统时钟，HCLK是高速外设时钟，是给外部设备的，比如内存，flash。

**APB1**：低速外设，连接的设备有CAN、USB、I2C1、I2C2、UART2、UART3、SPI2、看门狗、Timer2、Timer3、Timer4。

**APB2**：高速外设，连接的设备有：UART1、SPI1、Timer1、ADC1、ADC2、所有普通IO口(PA~PE)、第二功能IO口。

### 项目管理

这个页面可以进行项目与代码生成时相关的配置：

![project_manager_01](http://robofuture.net.cn/assets/images/STM32CubeIDE/project_manager_01.png)

![project_manager_02](http://robofuture.net.cn/assets/images/STM32CubeIDE/project_manager_02.png)

![project_manager_03](http://robofuture.net.cn/assets/images/STM32CubeIDE/project_manager_03.png)

###  工具

这个页面主要进行功耗模拟：

![tool_configuration](http://robofuture.net.cn/assets/images/STM32CubeIDE/tool_configuration.png)

## 引脚配置

前面我们简单了解了STM32CubeMX的界面，接下来我们来进行简单的配置。这里我们使用的开发板为RoboMaster 开发板A型，先获取[用户手册与原理图](https://www.robomaster.com/zh-CN/products/components/general/development-board)。

### SWD配置

新建一个项目，我们首先配置调试引脚，查看手册，开发板A型使用的是 SWD 调试接口：

![A-SWD](http://robofuture.net.cn/assets/images/RoboMasterDevelopmentBoard/A-SWD.png)

因此我们选择SYS ->Debug->Serial Wire，如下图，PA13、PA14 就配置成了调试接口：

![SWD](http://robofuture.net.cn/assets/images/STM32CubeIDE/SWD.png)

### 时钟配置

接着配置时钟，我们查看原理图，开发板使用了一个 12MHZ 的晶振：

![A-HSE](http://robofuture.net.cn/assets/images/RoboMasterDevelopmentBoard/A-HSE.png)

因此，我们进行配置，RCC->High Speed Clock->Crystal/Ceramic Resonator，如下图，PH0 与 PH1 配置为了晶振引脚：

![HSE](http://robofuture.net.cn/assets/images/STM32CubeIDE/HSE.png)

然后我们进入 Clock Configuration 界面，按如下顺序进行如下配置：

![A-ClockConfig](http://robofuture.net.cn/assets/images/RoboMasterDevelopmentBoard/A-ClockConfig.png)

### 点亮 LED

最后我们根据项目配置应用引脚，这里我们使用LED进行演示，查看用户手册，开发板一共有10颗 LED，这里我们使用 PF14 和 PE11 引脚的LED：

![A-LED](http://robofuture.net.cn/assets/images/RoboMasterDevelopmentBoard/A-LED.png)

先选择 Pinout view 中的引脚，选择 GPIO_Output，配置成输出模式，再选择左侧的 GPIO 对配置的功能进行修改，文档中说明引脚高电平时灯才熄灭，因此我们在 GPIO output level 中配置成 High，这样上电后 LED 一开始就是熄灭的了，我们还可以修改 User Label，定义一个用户标签，在后面编写程序时会用到：

![LED_config](http://robofuture.net.cn/assets/images/STM32CubeIDE/LED_config.png)

打开 main.c 文件编写代码，注意，我们的代码需要在 `/* USER CODE BEGIN xxx */ `与` /* USER CODE END xxx */`之间，不然下次生成的时候会被删除，我们编写一个交替闪烁的程序，如下：

![LED_code](http://robofuture.net.cn/assets/images/STM32CubeIDE/LED_code.png)

编写完程序后，我们进行编译![build_button](http://robofuture.net.cn/assets/images/STM32CubeIDE/build_button.png)，运行![run_button](http://robofuture.net.cn/assets/images/STM32CubeIDE/run_button.png)，调试![debug_button](http://robofuture.net.cn/assets/images/STM32CubeIDE/debug_button.png)，来烧录与运行程序。