---
title: Git的使用与Gitflow开发流程
date: 2026-1-3 19:45:10
tags: 学习
categories: Java开发
cover: /medias/Git.png
---

# Git的使用与Gitflow开发流程

# 一.Git下载安装

## 1.Git下载

**(1)去官网下载git软件，安装软件的一系列操作**

之后参考黑马的视频讲解进行一些账号信息的初始化，以及生成密钥等等，这些是后续从github或者gitee上推送或者拉取代码的关键。

{% asset_img image-20251121213851949.png%}

**(2)安装完成后，在cmd中输入如下指令：git --version，出现git版本信息，说明安装成功**

{% asset_img image-20251121213948869.png%}

**或者安装完成后在任意文件夹内部单击右键，如果能够看到如下两个菜单则说明Git安装成功**

{% asset_img image-20260103190549798.png%}

## 2.基本信息配置

**基本信息设置**

```bash
git config --global user.name “itcast”//引号内部表示自定义的用户名
git config --global user.email “hello@itcast.cn”//引号内部表示用户的邮箱
```

**基本信息查看**

```bash
git config --global user.name
git config --global user.email
```

## 3.SSH公钥-生成，查看与配置

**要想通过SSH地址克隆项目，必须提前在代码托管平台中配置你自己的git密钥，才有权限拉到本地**

**下面的操作都在Git Bash here中进行**

**（1）生成SSH公钥**

```cmd
ssh-keygen -t rsa
```

不断回车；如果公钥已经存在，则自动覆盖。

**（2）查看SSH公钥**

```cmd
cat ~/.ssh/id_rsa.pub
```

**（3）验证公钥是否在托管平台配置成功**

```cmd
ssh -T  git@gitee.com
```

```cmd
ssh -T  git@github.com
```

```cmd
ssh -T  git@192.168.150.101
```

{% asset_img image-20260103192708730.png%}

**gitee配置公钥:**

{% asset_img image-20260103192924694.png%}

**github配置公钥**：

{% asset_img image-20260103193012327.png%}

{% asset_img image-20260103193021694.png%}

{% asset_img image-20260103193032850.png%}

**♥用SSH验证公钥时**

{% asset_img image-20260103193141397.png%}

## 4.创建仓库并推送常用指令

git把资源推至github/gitee，下面代码适用与第一次推送，后续再推送，只需add,commit -m,push即可

在需要推送的文件夹内部，鼠标右键并选择Git Bash here，并在终端逐条输入下面的指令

```cmd
# 初始化 Git
git init
# 添加所有文件
git add .
# 提交
git commit -m "Initial Hexo project"#引号内的内容是推送的注释
# 关联远程仓库
git remote add origin https://github.com/chaogelinjia/hexo-blog.git
#git remote add用于创建远程仓库,origin远程仓库的名字,后面跟远程仓库地址
# 推送
git push -u origin main
#将本地main分支的代码推送到远程仓库origin的main分支，并建立跟踪关系
```

```cmd
# 之后可以简写为：
git push    # 自动推送到 origin/main
git pull    # 自动从 origin/main 拉取
```

# 二.子分支develop

**在本地开发环境创建develop分支**

{% asset_img image-20260103174238124.png%}

{% asset_img image-20260103174255294.png%}

{% asset_img image-20260103174421199.png%}

此时，只有本地有develop分支，远端还没有，所以需要进行一次推送

{% asset_img image-20260103174445265.png%}

**推送完毕**

{% asset_img image-20260103174534224.png%}

# 三.开发分支feature

**基于develop分支创建feature分支**

{% asset_img image-20260103174920629.png%}

{% asset_img image-20260103175309199.png%}

# 四.合并分支

**1.先将feature-mul代码提交到本地仓库 git commit**

**2.然后，切换分支（check out）到develop分支，此时develop分支内部并没有开发分支feature-mul的代码，需要进行合并**

**3.在feature-mul处，鼠标右键，选择将feature-mul合并到develop中，这个时候feature-mul中新增的代码就会加入到develop中**

**4.开发完成之后，再将本地的develop分支推送到远端的origin/develop分支里面**

**5.合并并推送到远端之后，开发分支feature-mul就可以删除了，不需要推送，因为功能已经合并进develop，他的任务结束了。**

{% asset_img image-20260103175750978.png%}

{% asset_img image-20260103180049206.png%}

# 五.切换分支

右键需要切换到的分支，然后选择check out(签出，即可完成分支切换)

{% asset_img image-20260103174816860.png%}

# 六.Release分支

**在develop分支开发基本上结束后，将基于develop分支创建release分支，在此分支进行测试，测试完成后合并到master和develop分支**

{% asset_img image-20260103180750905.png%}

创建分支后，进行模拟测试和bug修复后，提交代码：

{% asset_img image-20260103181043079.png%}

{% asset_img image-20260103181052572.png%}

**远端成功新增了release-v1.0分支**

{% asset_img image-20260103181138569.png%}

**所有测试完成后，将release分支合并回master和develop，并且推送到远程仓库。**

**先check out到要合并进的分支，然后进行merge合并**

{% asset_img image-20260103181309993.png%}

# 七.发布并打标签

{% asset_img image-20260103181801691.png%}

{% asset_img image-20260103181820786.png%}

{% asset_img image-20260103181841400.png%}

**创建完标签后进行推送**

{% asset_img image-20260103182133121.png%}

**推送成功**

{% asset_img image-20260103182210631.png%}