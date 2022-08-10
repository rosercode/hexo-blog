---
title: Ubuntu20.04 | 重装系统后要做的几件事情
date: 2021-06-13 12:12:29
tags:

---

Ubuntu20.04 | 重装系统后要做的几件事情 (๑•̀ㅂ•́) ✧

<!-- more -->

2021-06-11 号 ，我把自己的 笔记本电脑 重装了系统，重新安装了一些软件，简单的记录一下过程，

下一次重装系统时，再装软件会快一下。

这里就 Ubuntu20.04 进行配置

## ssh

更换 Ubuntu 默认的 apt 源

```shell
sudo apt install ssh
```

一个安全的远程终端协议

值得注意的是：

这么一个常用的工具，在几乎所有的 Linux 发行版上都不带有这个这个工具，而在 Windows10 中却默认带有这个工具	

## net-tools

```shell
sudo apt install net-tools
```

网络工具包，Linux 中常用的网络命令都在这个包中，如  ifconfig、netstat 等等网络命令

但是 Ubuntu 默认是没有带有这个工具包

## vim

```shell
sudo apt install vim
```

vim 一个文本编辑器

```shell
sudo dpkg -i google-chrome-stable_current_amd64.deb
```

apt 源中似乎没有这个浏览器、在官网下载对应的 deb 包进行安装

## pip3

```shell
sudo apt install python3-pip	
```

ubuntu 默认是带有 python3，但是默认是没有带有 pip3 这个包管理

```shell
pip3 config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```

更改 pip3 这个包管理对应的源

```shell
pip3 install you-get
```

安装 you-get 这个好用的视频下载工具

```shell
sudo pip3 install jupyter
```

在某些方面， jupyter 是很多优点的

PS：安装是比较难进行安装的、估计是因为软件太大了，和网络的问题而导致频繁安装失败 (图书馆的网络就是差，新疆的网络...)

## typora

```shell
 sudo snap install typora
```

虽然我并不是很喜欢snap、这个 Ubuntu  默认提供的包管理工具，但是自己更不喜欢去管理添加 apt 源，在使用 apt 来安装这个软件

习惯了使用 包管理 去安装软件，就不想在去 “官网” 去安装软件了

- 国内没有对应的镜像源，官方的源下载软件是很慢的
- 使用 snap 安装的软件，启动的速度是稍微有点满的，不过在使用上，和其它安装方式安装的基本上没有什么不同
- snap 是磁盘单独划分一个分区来安装软件，这样解决了 Linux 的依赖问题，但是很“难看”

而下面是官方提供的一种安装 typora 的安装方式(推荐):

```shell
# or run:
# sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys BA300B7755AFCFAE
wget -qO - https://typora.io/linux/public-key.asc | sudo apt-key add -
# add Typora's repository
sudo add-apt-repository 'deb https://typora.io/linux ./'
sudo apt-get update
# install typora
sudo apt-get install typora
```

## 网易云音乐

```shell
sudo dpkg -i netease-cloud-music_1.2.1_amd64_ubuntu_20190428.deb 
```

网易官方提供的 Linux 的网易云音乐客户端

```shell
 sudo apt-get install gnome-tweak-tool
 sudo apt-get install gnome-shell-extensions
```

需要安装 Ubuntu的一些插件

## wps

```shell
sudo dpkg -i wps-office_11.1.0.10161_amd64.deb 
```

虽然 Linux 的 WPS 有各种问题，但是我并没有找到其它的、好用的、同类型的软件

## 网络工具

```shell
sudo apt install nmap
```

虽然自己不做有关 网络安全 方面的事情，但毕竟自己是学网络的，还是需要 namp 这个软件

```shell
 sudo apt install netwox
```

netwox 也是一款和 网络安全 相关的软件

```shell
sudo apt-get install wireshark
```

一款出色的抓包软件

## 输入法

```shell
sudo dpkg -i sogoupinyin_2.4.0.3469_amd64.deb 
```

想更换一个输入法，但是在暂时没有找到和 搜狗 相近的输入法

## vlc

```shell
sudo apt install vlc
```

vlc 、造成我第一个 Linux 系统 deepin 的桌面(dde)，被删掉的根本原因

谁它的知道，dde 这个桌面依赖于 vlc-data 这个包

在 Ubuntu 中，你要关闭 vlc，还不能直接在软件的界面右上角进行关闭



安装 Ubuntu 的插件 dash to dock 这个托盘插件

在使用这个插件时，屏幕一锁定在重新启动时，就会出现 Ubuntu 原本的 dock 和 dash to dock 相重叠的问题

解决方法查看[这里](https://www.jianshu.com/p/c152e56c7a0a)

- 执行下面的命令可以解决问题，本质上是把 Ubuntu 原生的 dock 移除掉

```shell
cd /usr/share/gnome-shell/extensions/
sudo mv ubuntu-dock@ubuntu.com{,.bak}
```

- 如果想要使用原本的 dock，只需把扩展名修改回来就可以了

```shell
cd /usr/share/gnome-shell/extensions/
sudo mv ubuntu-dock@ubuntu.com{.bak,}
```

PS：在上一个  Ubuntu 系统中，我应该是解决了这个问题，不过我忘记了是怎么解决这个问题的

或者

```shell
sudo mv /usr/share/gnome-shell/extensions/ubuntu-dock@ubuntu.com ~/
或者
sudo rm -rf /usr/share/gnome-shell/extensions/ubuntu-dock@ubuntu.com
```

<div align="right">
    <a href="https://www.jianshu.com/p/8bf28040ab43">连接</a>
</div>



[Ubuntu20.04 添加右键新建文件](https://blog.csdn.net/qq_45683435/article/details/108961947)

默认是什么有没有的，安装完 WPS 后，会在用户的家目录创建一个名为 Templates 目录，并在这个目录中添加对应的文件

添加了  markdown 和 txt 这两种常用的文件格式

PS：只是创建一个文件就要打开一个终端、输入一个命令来进行文件的创建

## utools

```shell
sudo dpkg -i utools_1.3.5_amd64.deb 
```

安装 [utool](https://u.tools/) 这个工具，utool 提供的这个一些插件还是真的好用，对我而言，最有用的插件就是 **内网穿透** 这个插件了

同时创建开机自启动，具体的过程参看 [这里](https://blog.csdn.net/qq_39902475/article/details/108238901)

简单来说，就是添加启动 utools 的命令(utools)到  startup application 中



安装 Joplin 和 Obsidian(黑曜石) 这两款笔记软件

并创建对应的 applications 上的 logo

安装 mc 这款沙盒游戏，并创建对应的 applications 的 logo

```properties
[Desktop Entry]
Type=Application
Name=Joplin
Exec=/home/test/jobs/Joplin/Joplin-1.0.220.AppImage
Icon=/home/test/jobs/Joplin/Joplin.png
Categories=development;IDE;
Terminal=false
```



使用 [rsync](http://www.ruanyifeng.com/blog/2020/08/rsync.html)  这个命令行工具来备份文件

## drawio

```shell
sudo snap install drawio
```

drawio 一款出色的绘图软件

## filezilla

```shell
sudo apt install filezilla
```

一款 FTP 和 SFTP 的工具



## okular

```shell
 sudo apt-get install okular
```

一个 PDF电子书阅读的软件，这个软件挺大的

在 [这里](https://zhuanlan.zhihu.com/p/53298578) 推荐了一些 Linux 平台的 PDF 阅读软件

## calibre

```shell
sudo apt install calibre
```



## mcomix

```shell
sudo apt install mcomix
```

简单一个看漫画的软件，上面的使用 Ubuntu 的 APT 的包管理进行安装的，

也可以在 [这里](https://pkgs.org/download/mcomix) 下载对应的 deb 包进行安装，在 [这里](https://pkgs.org/download/mcomix) 提供了所有平台的 deb 包



## flameshot

```shell
sudo apt install flameshot
```

一款好用的截图软件，相关的配置可参考 [这里](https://zhuanlan.zhihu.com/p/166559142)，GitHub的地址可在 [这里](https%3A//github.com/lupoDharkael/flameshot) 找到

这款软件还是值得我推荐的

## peek

```
sudo apt install peek
```

## steam

虽然很少在 steam 上玩游戏，但是还是应该安装上的

```shell
sudo apt install curl
sudo dpkg -i steam_latest.deb 
```

你可以在 [官网](https://store.steampowered.com/) 进行 [下载](https://media.st.dl.pinyuncloud.com/client/installer/steam.deb) 对应的 deb 包就可以了

具体的安装过程，在 2021-06-17 的 diary 记录，内容过多，就不是说明了

## ffmpeg

```	shell
sudo apt install ffmpeg
```

## VmWare

```shell
chmod +x VMware-Workstation-Full-16.1.2-17966106.x86_64.bundle 
sudo ./VMware-Workstation-Full-16.1.2-17966106.x86_64.bundle 
```

PS:使用 VMWare 安装虚拟机时，虚拟内存要分配打一点；在安装完成后可以降下来

Ubuntu 在浏览器访问 网站 时，反应特别慢，可尝试绑定一个静态的 DNS 服务器就可以了；参考至[这里](https://blog.csdn.net/zZzZzZ__/article/details/102518218)

同时，[这里](https://blog.csdn.net/zyh821351004/article/details/43699887) 和 [这里](https://blog.csdn.net/weixin_46036722/article/details/113179049) 提供了安装 dnsmasq 这个软件的方式来增快网站的反应

## ranger

```shell
sudo apt-get install ranger
```

## mysql-server

```shell
sudo apt-get install mysql-server
```

## 7zip

```shell
sudo apt install 7zip
```

一款解压软件



## ark

```shell
sudo apt install ark
```

Linux 平台一款解压和压缩软件

Ubuntu 默认带有的相关软件各种问题

https://www.cnblogs.com/santiaoa/p/5846158.html



```shell
sudo apt install dconf-editor
```

导航到**org> gnome> shell>扩展> dash-to-dock**并检查**isolate-workspaces







