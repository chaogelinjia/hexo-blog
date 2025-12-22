---
title: labelimg安装
date: 2025-12-21 12:28:05
tags: 学习
categories: 深度学习
cover: /medias/labelimg安装.png
---

# labelimg安装

## 一.labelimg安装

**1.进入anaconda prompt创建一个新的虚拟环境，命名为label,并且python版本为3.9**

```bash
conda create -n label python==3.9
```

**2.进入label虚拟环境，安装labelimg**

```bash
conda activate label
```

```bash
pip install labelimg
```

**3.进入label虚拟环境，打开labelimg软件**

label环境内，输入命令:labelimg即可打开标注软件

```cmd
labelimg
```

{% asset_img image-20251220160459054.png%}

## 二.labelimg进行标注

{% asset_img image-20251220160559196.png%}

**第三个:change Save Dir用来更改图片标注完之后，标签信息的存放位置即xml文件**

{% asset_img image-20251220160620632.png%}

{% asset_img image-20251220160626765.png%}

{% asset_img image-20251220160632060.png%}

{% asset_img image-20251220160637099.png%}

**2中存放的为所要进行标注的图片，1中存放的为对2中的图片进行标注完成之后生成的所有标签信息，3为标注所需要的所有类别信息**

{% asset_img image-20251220160702586.png%}

{% asset_img image-20251220160707068.png%}

{% asset_img image-20251220160712751.png%}

{% asset_img image-20251220160717111.png%}
