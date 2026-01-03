---
title: Pytorch 环境搭建
date: 2025-11-24 14:44:54
tags: 学习
categories: 深度学习
cover: /medias/pytorch.png 
---

# 最详细Pytorch环境搭建全流程

## 一.Pycharm安装

Pycharm是最主流的python代码编辑器，往后进行深度学习代码的编写均在这个软件进行。本电脑版本2024.1

## 二．anaconda安装以及创建虚拟环境

### **（1）anaconda安装**

1.   anaconda版本选用2022.10,目前最稳定，而且后期安装第三方库时，会联网下载，所以更新的包依然可以下载，因此anaconda2022.10永不过时。

2.   为什么要下载anaconda?

首先，anaconda本身含有python.exe即python解释器，不需要单独下载python解释器；同时anaconda里面内置了很多第三方库，便于我们后期使用。

第二点，也是最重要的一点，anaconda可以根据不同的项目创建不同虚拟环境，很多项目所需要的包版本不同，而且依赖包之间有版本依赖关系，版本如果不对应，将导致程序无法运行。

{% asset_img image-20251124145630890.png%}

### **（2）配置环境变量**

因为命令行窗口是在c盘中运行，但是我们把anaconda安装在D盘，添加环境变量的作用在于，系统在命令行根据指令寻找所需要的文件过程中，会首先默认在C盘检索，如果没有，就会进入环境变量的Path路径（环境变量中的用户（仅当前用户可以使用）或者系统（使用当前系统的所有用户均可使用，电脑只有你个人使用所以没区别，我是安装在了系统环境变量中），检索，把anaconda相关路径添加的环境变量，便于后期命令行安装需要的包。（需要添加的有D:\develop\Anaconda，D:\develop\Anaconda\Scripts，D:\develop\Anaconda\Library\bin）

{% asset_img image-20251124145701528.png%}

{% asset_img image-20251124145719312.png%}

### **（3）anaconda创建虚拟环境**

1. 单机打开anaconda prompt程序（会直接进入base环境，也就是anaconda本身自带的基础环境）

2.

```
conda env list //列出目前拥有的所有虚拟环境（包括base环境）
```

```
conda create-n 环境名 python=3.9 //创建名为环境名的虚拟环境，并指定Python版本
```

eg:conda create-n DL python=3.9

环境会默认保存在Anaconda目录下的envs文件夹内部

```
conda activate 环境名 //激活当前环境，也就是进入当前环境
```

Eg: conda activate DL //进入DL虚拟环境

```
conda env remove -n 环境名//删除该虚拟环境
```

3.虚拟环境内部的操作

```
conda list //列出当前虚拟环境下的所有库
```

```
conda deactivate//退出虚拟环境到base环境中
```

剩下就是在虚拟环境下安装所需库的指令了

{% asset_img image-20251124145751123.png%}

## 三.Pytorch安装

### **1.**显卡相关概念：

(1)显卡是计算机的一个处理图片的高性能芯片（必须是英伟达的独立显卡才可以提高深度学习训练算力—属于硬件范畴,Intel英特尔的核显不可以用来加速深度学习训练）。

(2)显卡驱动（CUDA driver version）用于让计算机能够识别出显卡的存在。--去英伟达官网安装电脑显卡硬件所对应的最新版本驱动。

(3)显卡运行程序（cuda runtime version）,pytorch利用cuda runtime version去调用显卡驱动去驱动显卡，利用显卡算力加速训练（利用显卡进行并行运算）。

总结:CUDA driver（CUDA驱动版本）要高于cuda runtime 的版本。

### **2.cuda**相关程序安装的保姆级教程

安装cuda最简单教程

1.将显卡驱动更新到最新版本:（CUDA drive version,硬件买来是固定,只能更新驱动，为后面安装cuda做准备，因为CUDA驱动版本要≥cuda runtime version,更新到最新可以增加cuda选择范围，最大化利用算力）

快捷键ctrl+shift+esc打开任务管理器，查看本机电脑的显卡格式，再去英伟达官网下载对应的最新驱动。

{% asset_img image-20251124145801944.png%}

{% asset_img image-20251124145811291.png%}

{% asset_img image-20251124145819578.png%}

{% asset_img image-20251124145832685.png%}

英伟达网址:https://www.nvidia.cn/

下载并安装驱动（建议C盘默认位置）

2.查看安装好的显卡驱动（为后续安装Pytorch以及cuda版本做准备）

打开命令行窗口win+r，输入cmd回车。输入nvidia-smi来确定目前CUDA driver驱动版本（我的是12.9版本）

{% asset_img image-20251124145940407.png%}

### 3.安装合适版本的Pytorch

打开Pytorch官网，选择兼容的cuda runtime（gpu计算平台）版本进行安装。（浏览器的快捷键ctrl+f搜索，可以快速检索到我们需要的版本。（因为我的显卡驱动版本是12.9，所以cuda runtime版本小于12.9即可，我这里选择cuda12.6版本）

安装Pytorch包其实包括三部分:pytorch,torchvision,torchaudio

Pytorch官网:

https://pytorch.org/

注意⚠️:

（1）conda安装容易出问题，推荐pip安装（官网也下架了conda安装选择）

（2）CUDA驱动安装，选择game ready游戏版驱动就可以

（3）终止命令行的安装命令:ctrl+c或者直接把命令行窗口关闭。

{% asset_img image-20251124150007188.png%}

**通过anaconda prompt命令行窗口，进入需要安装Pytorch的虚拟环境（conda activate xx），将Run this command的这段命令复制粘贴回车即可完成安装。（现在官方已经将默认下载地址调整至NVIDIA官方路径，所以下载速度很快，不需要在-c选择镜像源安装了，用镜像源安装，反而会出错。**

{% asset_img image-20251124150018807.png%}

**看到Successfully,即Pytorch库安装成功。**

### 4.检验Pytorch是否安装成功

{% asset_img image-20251124150102973.png%}

{% asset_img image-20251124150108199.png%}
