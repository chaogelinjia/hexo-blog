---
title: 从0-1在Pycharm中复现项目
date: 2025-12-21 12:28:05
tags: 学习
categories: 深度学习
cover: /medias/Pycharm配置深度学习论文环境.png
---

# 从0-1在Pycharm中复现项目

## 一.从Pycharm中打开项目

Step1:从github等开源网站下载源代码到本地

Step2: 在pycharm中打开项目

{% asset_img image-20251220154601276.png%}

{% asset_img image-20251220154612381.png%}

## 二．创建虚拟环境

1.创建虚拟环境，并根据需要选择合适的python版本

（进入Anaconda prompt操作）

（1）conda env list 查看现有虚拟环境

（2）conda create -n weban python=3.11 创建名为weban的虚拟环境，并且为3.11版本的python环境

（3）conda activate weban 激活虚拟环境（进入虚拟环境）

（4）其中requirements.txt中写了项目所需要的所有依赖包的版本，需要安装金weban虚拟环境

**法一：选择性安装：**

conda activate weban进入虚拟环境后，输入pip install 依赖包，进行安装。（逐个安装）。

**法二：根据requirement.txt一键安装**

conda activate weban 进入虚拟环境后（一定要先进入运行程序的虚拟环境），然后通过cd命令，进入requirement.txt所在目录。

然后通过pip install -r requirements.txt （-r就是读取，命令用来读取文件中的所有包，并进行安装。）

{% asset_img image-20251220154710926.png%}

{% asset_img image-20251220154718873.png%}

{% asset_img image-20251220154724892.png%}

{% asset_img image-20251220154731016.png%}

## 三．选择并配置虚拟环境

### 1.设置-项目-python解释器-添加本地解释器

{% asset_img image-20251220154757535.png%}

### 2.conda环境选择时，选择condabin目录下的conda.bat才能扫描到所有虚拟环境

{% asset_img image-20251220154816841.png%}

### 3.添加并选择虚拟环境

{% asset_img image-20251220154828334.png%}

{% asset_img image-20251220154836093.png%}

### 4.运行主程序，后续根据日志进行排错即可

{% asset_img image-20251220154849758.png%}