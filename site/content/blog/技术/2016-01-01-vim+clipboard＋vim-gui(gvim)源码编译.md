
---
title: vim+clipboard＋vim-gui(gvim)源码编译
date: 2016-01-01 18:02:23 +0000 UTC
description: 昨天因为系统中自带的vim中没有clipboard特性,别的程序到vim中粘贴复制内容比较别扭。于是就（ˇˍˇ）　想～从重新编译一个完整版本的vim。于是就倒弄了一天。。。。。。　　　　　　   首先先贴下环境：Fedora 22 +gcc 5.3.1版本＋vim74源码包首先下载vim74源码包,这个可以到vim.org官网下载,这里我贴出linux需要下载的版本(也是我下载的版本)的链接:h
---
>  昨天因为系统中自带的vim中没有clipboard特性,别的程序到vim中粘贴复制内容比较别扭。于是就（ˇˍˇ）　想～从重新编译一个完整版本的vim。于是就倒弄了一天。。。。。。　　　　　　
> 首先先贴下环境：Fedora 22 +gcc 5.3.1版本＋vim74源码包


----------


```
首先下载vim74源码包,这个可以到vim.org官网下载,这里我贴出linux需要下载的版本(也是我下载的版本)的链接:https://github.com/vim/vim.git(这是vim在github下托管的链接)
```

```
你只需要:
cd yourdir/youdir/youdir
git clone https://github.com/vim/vim.git
将源码下下来
```

> 然后进入你下载的源码目录,如果你没改目录名的话,应该是当前目录下的vim文件夹内(如下图)

![vim源码目录](http://img.blog.csdn.net/20160101171022811)

> 然后安装编译vim-gui(gvim)需要的gui环境依赖头文件,可以是gtk2,gnome....等等.(我安装的是gtk2)

```
Fedora下用yum安装:
sudo yum install  gtk2-devel.x86_64 (这里看你的系统版本,如果是32位的,就装gtk2-devel.i686 这个包,我的系统是64位的,我这里是安装gtk-gui,如果你是安装其他gui的话,需要安装其他的包而不是这个包)
...
注意:不同的软件源的包名可能不一样,大家可以用**yum search+关键字**搜一下，名称应该类似
```

> 接下来还要安装
>     libXt-devel.x86_64 
>     libX11-devel.x86_64 
>     这两个包都是X11图形界面的源码包`

```
sudo yum install libXt-devel.x86_64 && sudo yum install  libX11-devel.x86_64
...

>libXt-devel.x86_64这个包是让我折腾一天的罪魁祸首,哭晕。。。,你也可以直接安装qt3-devel.x86_64这个包,它包含了libXt-devel.x86_64。

```

> 好了,现在你可以编译源码了,进入源码包


```
cd  vim 或者cd vim/src
./configure　--with-features=huge | grep gui(这里我选择带特征最多的巨型版本,--with-features=normal(正常版本),--with-features=tiny(微型版本),默认是正常版本)
```
![这里写图片描述](http://img.blog.csdn.net/20160101174448504)

> 如果你显示这个的话，说明你的gui可以用，也就是能编译出vim-gui和clipboard否则不行（按理说clipboard这个特性应该不会依赖gui，但是我gui编译不出,clipboard特性也编译不出）,编译出来的朋友们可以私信我，是怎么回事,我也学习学习。
> ...
>注意：vim编译的时候默认的gui配置选项为- -enable-gui=auto，这样系统会自动搜索是否支持编译成gvim，可以就编译,否则就忽略。当然你也可以指定特定的gui。
>...
>- -enable-gui=gtk2
...
不过建议使用默认的

```
sudo make && sudo make install (编译链接不多说了)
```

```
如果没出问题的话就可以使用了,如果有的出现问题,也就是有些包没装，装下依赖包就可以了。(yum search & yum install )
```

> 现在可以看看我们编译后的成果了。
> gvim 或　vim -g
> 看看gvim怎么样

![这里写图片描述](http://img.blog.csdn.net/20160101175916541)

> vim --version
> 看看vim
> ![这里写图片描述](http://img.blog.csdn.net/20160101180021590)

```
现在是巨型版本,clipboard特性也有了。success！
```
