---
title: Hexo+github搭建个人专属博客
date: 2025-12-20 12:28:05
tags: 学习
categories: 博客相关
cover: /medias/Hexo.png
---

# Hexo+github搭建个人专属博客

## 一.基础环境配置

### 1.git下载与安装

**(1)去官网下载git软件**，之后参考黑马的视频讲解进行一些账号信息的初始化，以及生成密钥等等，这些是后续从github或者gitee上推送或者拉取代码的关键。

视频链接如下：

【黑马程序员Git全套教程，完整的git项目管理工具教程，一套精通git】 https://www.bilibili.com/video/BV1MU4y1Y7h5/?p=5&share_source=copy_web&vd_source=aea6b8ca9dfcd60d1a152bd9497b5c60

{% asset_img image-20251121213851949.png%}

**(2)安装完成后，在cmd中输入如下指令：git --version，出现git版本信息，说明安装成功**

{% asset_img image-20251121213948869.png%}

### 2.Node.js下载与安装

**(1)浏览器搜索进入Node.js官网，下载对应的安装文件（LTS为长期支持版，更稳定）**，

{% asset_img image-20251121214115221.png%}

**(2)除了需要修改一下安装路径外（我习惯放在D盘），其他安装进程，一路next即可**

**(3)等待安装完成，在cmd中输入如下指令：node -v，出现node.js版本信息，说明安装成功**

{% asset_img image-20251121214455587.png%}

#### 2.1 Node.js环境配置

##### 2.1.1 配置全局安装的模块路径和缓存路径

**（1）创建文件夹目录，在nodejs根目录,创建`node_global`，`node_cache`文件夹**

{% asset_img image-20251121214749711.png%}

**（2）管理员身份- 打开CMD，配置路径：（注意一定要管理员身份运行CMD！！！路径改成你自己的路径，不要无脑复制！！！）**

```bash
npm config set prefix "D:\develop\Node\anzhuang\node_global"
npm config set cache "D:\develop\Node\anzhuang\node_cache"
```

##### 2.1.2 配置环境变量

win10&win11：右键此电脑——属性——高级系统设置——高级——环境变量

{% asset_img image-20251121215108567.png%}

**（1） 创建 NODE_HOME 变量**

**变量值为nodejs的安装地址**

{% asset_img image-20251121215212197.png%}

**（2）在 系统变量 中 选择 Path 修改和添加如下属性：**

{% asset_img image-20251121215345035.png%}

**添加`node_global`，`node_cache`：**

{% asset_img image-20251121215403769.png%}

#### 2.2 测试效果

**全局安装最常用的 express 模块 进行测试**
**命令如下:**

```bash
npm install express -g
```

{% asset_img image-20251121215523560.png%}

#### 2.3 全局配置淘宝镜像

**注意一定要管理员身份运行CMD！！！**

```bash
npm config set registry https://registry.npmmirror.com
```

**安装cnpm(安装Hexo框架要用到)**

```bash
npm install -g cnpm
```

**查看配置**

```bash
npm config ls
```

{% asset_img image-20251121215806753.png%}

### 3.安装Hexo框架

（1)**命令行中通过 cnpm install 命令安装您想要的程序，可在 cmd 中输入cnpm -v, 出现cnpm 版本信息说明安装成功**

{% asset_img image-20251121220135584.png%}

**注意：本教程所有用到cmd的都必须要以管理员身份运行才可以，下图展示如何在电脑上以管理员身份运行**

{% asset_img image-20251121220105400.png%}

**(2) 安装hexo**

```bash
cnpm install -g hexo-cli
```

**可在 cmd 中输入 hexo -v, 出现hexo版本信息说明安装成功**

{% asset_img image-20251121220413576.png%}

### 4.使用Hexo搭建博客

**4.1  建立存放hexo项目的文件夹，我放在了D盘的Hexo文件夹内部，刚开始里面什么都没有，图片的这些内容是后续操作才产生的**

{% asset_img image-20251121220614314.png%}

**4.2 在该文件夹(D:\Hexo)下右键选择Open Git Bash here,图示为安装目录**

{% asset_img image-20251121220742966.png%}

**4.3 在git窗口，输入：hexo init，进行项目的初始化**

{% asset_img image-20251121220824353.png%}

**4.4 初始化完成后，在存放项目的文件夹中会出现以下配置文件** 

{% asset_img image-20251121220900832.png%}

**4.5 在git窗口，输入:hexo s,开启本地预览服务，打开浏览器访问 [http://localhost:4000](https://link.zhihu.com/?target=http%3A//localhost%3A4000/) 即可看到博客内容**

{% asset_img image-20251121220930305.png%}

**页面效果图如下：**

{% asset_img image-20251121220945023.png%}

**至此，博客网站已经初步配置成功**

### 5.更换主题

主题文件存放在themes文件夹下

**5.1 主题搜索**

hexo 官方网站，[Themes | Hexo](https://hexo.io/themes/)，点击名字即可跳转进入github网站

{% asset_img image-20251121221105318.png%}

**5.2 主题下载**

**（1）获取喜欢的hexo主题的http链接和主题名**

{% asset_img image-20251121221231803.png%}

**（2）在项目文件夹下，使用Open Git Bash here打开git窗口，输入以下指令**

**在这个文件夹内部，单机鼠标右键，进入Git Bash here入口**

{% asset_img image-20251121221353573.png%}

```
git clone git@github.com:jerryc127/hexo-theme-butterfly.git hexo-theme-butterfly
```

**（3）主题下载完毕，在themse文件夹下会出现名为：[hexo-theme-butterfly](https://github.com/denjones/hexo-theme-chan)的主题文件夹**

{% asset_img image-20251121221353573-1766062095534-28.png%}

**（4）打开Hexo根目录下的_config.yml文件，将theme: landscape改为theme: hexo-theme-butterfly用于切换主题**

**也就是说根据themes文件夹内部的文件夹名字来选择对应的主题渲染。**

**（5）然后在git Bash here窗口，输入以下指令，打开浏览器访问 [http://localhost:4000](https://link.zhihu.com/?target=http%3A//localhost%3A4000/) 即可看到新的博客主题**

```cmd
hexo clean //执行此命令后继续下一条
hexo g //生成博客目录
hexo s //本地预览，这一步就可以观看本地运行效果了
hexo d //部署到github上--上传到仓库的是生成好的静态页面而不是源码
```

**生成butterfly主题博客展示**

{% asset_img image-20251122073852585.png%}

**注意：**

**要想获取SSH克隆地址，必须提前在github中配置你自己的git密钥**

默认已经提前生成好密钥，因为第一步git初始化中就有这个步骤。这里直接获取，下面的操作都在Git Bash here中进行

**step 1 获取密钥**

```bash
cd ~/.ssh
```

```bash
cat id_rsa.pub
```

{% asset_img image-20251121222021837.png%}

**step 2 github配置密钥**

**进入自己账号下的SettingI（右上角）**

{% asset_img image-20251121222050282.png%}

**然后点击SSH and GPG keys, 再点击New SSH key添加**

{% asset_img image-20251121222110191.png%}

**自己起个名，粘贴上面的内容，然后添加**

{% asset_img image-20251121222148699.png%}

**验证是否设置成功**（GIt Bash here中进行）

```bash
ssh -T git@github.com
```

第一次，可能不会直接显示成功，需要你给他一个指令：yes,后续他就会把这个信息存下来，不再会重复询问你了。如下显示

```bash
$ ssh -T git@github.com
The authenticity of host 'github.com (20.205.243.166)' can't be established.
ED25519 key fingerprint is SHA256:+DiY3wvvV6TuJJhbpZisF/zLDA0zPMSvHdkr4UvCOqU.
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])?
```

只需要回复：yes 即可！

**注意：**

git把资源推至github，下面代码适用与第一次推送，后续再推送，只需add,commit，mpush即可

```
# 初始化 Git
git init
# 添加所有文件
git add .
# 提交
git commit -m "Initial Hexo project"
# 关联远程仓库
git remote add origin https://github.com/chaogelinjia/hexo-blog.git
# 推送
git push -u origin main
```

国内网站如何不用科学上网，便可快速访问，详情请查看另一篇博文。

## 二. butterfly主题美化

**注意：**

**cmd中进入d盘的Hexo文件夹指令**

```bash
cd /d D:\Hexo
```

### 1.副标题

**themes-hexo-theme-butterfly-config.yml**

```yaml
# The subtitle on homepage
subtitle:
  enable: true 
  effect: true
  typed_option:
  source: 2
  sub: 
    - '纵有疾风起，人生不言弃'
```

### 2.图片与标题显示

**首先，需要修改Hexo目录下的config.yml的一些配置**

```yml
post_asset_folder: true
marked:
  prependRoot: true
  postAsset: true
```

当资源文件管理功能打开后，Hexo将会在你每一次通过 `hexo new a` 命令创建名为a的新文章时，会自动创建一个文件夹。 这个**资源文件夹将会有与这个文章文件一样的名字**。 **将所有与你的文章有关的资源放在这个关联文件夹中之后**，你**可以通过相对路径来引用它们**，这样你就得到了一个更简单而且方便得多的工作流。

**其次，修改typora的图像保存位置设置如下**

{% asset_img image-20251122153351815-1766062342182-37.png%}

**然后，在正常编写文章内容时，不需要管，会按照指定的保存路径保存图片**，但是这样上传到网站上是无法展示图片的。当文章全部完成之后，我们需要在每个图片的上面都按照下面的格式加上一行图片相关的markdown代码，加完之后，删除原先的图片，这样网站就可以根据markdown的asset_img标签插件解析渲染图片。

**正确的引用图片方式是使用下列的标签插件**

```bash
{% asset_img example.jpg%}
```

原图片markdown若为：

{% asset_img image-20251122153822566-1766063311811-2.png%}

改造后的依据标签插件的markdown代码如下--通过相对路径引用图片

```bash
{% asset_img image-20251122153351815.png%}
```

所有文章前面的**asset_img**都是不变的，只需要修改图片的文件名即可。

### 3.文章标题的显示

有时候我们完成了文章的编写以及图片的上传之后，发现在网站上的文章标题竟然是untitled，我们需要进行如下操作，

在文章最上方，**单机鼠标右键，插入Yaml Front matter**

{% asset_img image-20251122154417890-1766063382164-5.png%}

然后在这个框框里，按照规定格式命名标题

```bash
title: Hexo制作博客
```

这个文章的标题就会显示为Hexo制作博客

### 4.url的配置

在Hexo的根目录下的config.yml中修改url配置，改成自己**部署上线的网址名**

```yml
# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
url: https://cuicanxingheya1.netlify.app
```

### 5.butterfly主题

我们需要根据theme主题自己当初下载时定义的文件名(hexo-theme-butterfly,)把其内部自定义的配置文件_config.yml内容完整复制一份，并在Hexo文件根目录，创建一个新文件_config.hexo-theme-butterfly.yml，把刚才复制的主题内部的配置文件内容完整粘贴过去，这样再用Netlify部署上线的时，才能被正确解析，否则无法正常渲染。

{% asset_img image-20251122205330922-1766062392369-40.png%}

同时，D:\Hexo\themes\hexo-theme-butterfly\source\img文件夹内部，自定义加入的图片都要复制一份仅根目录的这个文件夹内部，才能被正确扫描部署：D:\Hexo\source\img

### 6.插入音乐

**(1) 安装 hexo-tag-aplayer 这款插件。执行如下指令：**

以超级管理员身份进入cmd,然后运行如下程序

```bash
npm install --save hexo-tag-aplayer
```

**(2) 修改或者加入一些配置信息**

下面这个配置信息需要添加在Hexo文件根目录下的_config.yml文件中，原始文件中没有

```yml
aplayer:
  meting: true
  asset_inject: false
```

修改如下内容

```yml
# Inject the css and script (aplayer/meting)
aplayerInject:
  enable: true
  per_page: true
```

以本博客为例，在博客Hexo的根目录下的source文件内部创建music文件夹并在其内部创建文件index.md文件路径如下（\source\music\index.[md文件](https://so.csdn.net/so/search?q=md文件&spm=1001.2101.3001.7020)）

**index.md内容如下：**

```bash
{% meting "1805939548" "netease" "song" "autoplay" "mutex:true" "listmaxheight:100px" "preload:none" "autoplay = true" "theme:#ad7a86"%}
```

"1805939548"网易云音乐的Id信息，"netease"代表网易云；"song"：song代表歌曲，playlist表示歌单

**(3) 全局吸底Aplayer播放器**

把下面的代码插入到主题配置文件的 inject.bottom下面即可。--利用vscode的ctrl+f快捷搜索定位

```yml
inject:
  head:
  bottom:
    - <div class="aplayer no-destroy" data-id="1805939548" data-server="netease" data-type="song" data-fixed="true" data-autoplay="true" data-lrcType="-1"> </div>
```

如果你想切换页面时，音乐不会中断。请把主题配置文件的 `pjax` 设为 true即可

```yml
pjax:
 enable: ture
 exclude:
```

### 7.添加live-2d模型

**（1）安装插件- Hexo-Helper-Live2D **

```bash
npm install --save hexo-helper-live2d
```

**（2）安装模型库**

用户可以通过安装不同的模型包来更换看板娘的模型。例如，安装 `live2d-widget-model-wanko模型：

```bash
npm install --save live2d-widget-model-wanko
```

**(3)在主题配置文件加入下面的信息**

{% asset_img image-20251222133934698.png%}

在全局配置文件.config.yml中最底部添加下面这段代码

```yml
live2d:
  enable: true #false表示不显示看板娘
  scriptFrom: local
  pluginRootPath: live2dw/
  pluginJsPath: lib/
  pluginModelPath: assets/
  tagMode: false
  log: false
  model:
    use: wanko   //选用的模型
  display:
    position: right
    width: 150
    height: 300
  mobile:
    show: false #false表示不在移动端显示
  react:
    opacity: 0.7
```

### 8.标签与分类

一个典型的 Hexo 博客目录：

{% asset_img image-20251124121053179-1766062417876-43.png%}

**（1）写文章的基本操作**

**创建一个文章文件**

```bash
hexo new post "我的第一篇文章"
```

生成的文件在 source/_posts/我的第一篇文章.md。

也可以直接把typora中的.md文件复制到hexo内部的source/_post目录内部，但是要在文章顶部加上Front-matter信息，该篇文章才能被hexo识别为博客文章并渲染。

**文章头部 Front-matter**

```bash
title: 微服务相关知识点及其组件
date: 2025-11-21 15:00:00
categories: Java开发
tags: 学习
```

```bash
title: Hexo+github搭建个人专属博客
date: 2025-12-20 12:28:05
tags: 学习
categories: 博客相关
cover: /medias/Hexo.png
```

**（2）导航栏标签跳转**

Hexo 不会自动生成 /categories/、/tags/、/archives/ 页面，需要手动新建：

```bash
hexo new page categories
hexo new page tags
hexo new page archives
```

生成的文件在 source/的对应文件夹内部，通过修改idex.md修改显示的内容

这样访问 `/categories/` 就能显示分类索引

同时如果你在菜单里配置了独立页面入口，都需要按照上面的操作在 `source/` 下新建对应文件夹：

**（3）在文章上加标签信息**

文章头部用Front-matter加入下面的内容，自行根据具体标签，分类信息进行修改

```bash
title: 微服务相关知识点及其组件
date: 2025-11-21 15:00:00
categories: Java开发
tags: 学习
```

**头部信息补充说明：**

置顶文章：在 Front-matter 加 `top: true`。

### 9.修改文章封面

在Hexo根目录下的source文件夹下创建一个medias文件夹，然后里面放入图片，在cover选项下: /img/图片名字，就可以引入

{% asset_img image-20251124141948792-1766062436323-46.png%}

```bash
title: 关于笔者
date: 2025-11-24 12:28:05
tags:
categories:
about: 笔者简介
cover: /medias/archive.jpg
```

效果如下：

{% asset_img image-20251124142231413-1766062456050-49.png%}
