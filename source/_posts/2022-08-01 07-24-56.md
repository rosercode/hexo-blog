---
title: Ubuntu 22.04 | Firefox 启动报错 "Failed to load module "canberra-gtk-module""
date: 2022-08-01 07:24:56
tags:

---

Ubuntu 22.04 | Firefox 启动报错 "Failed to load module "canberra-gtk-module""

<!-- more -->

![image-20220817142807815](../assets/image-20220817142807815.png)



## 引言

**Firefox** 是 绝大多数 **Linux** 发行版的默认浏览器

**Ubuntu** 默认（内置）提供的浏览器也是 **Firefox**，从 Ubutnu21.10 之后的版本，默认是以 **snap** 的方式安装的。

> Ubuntu 默认带有两个包管理器，snap 是 Ubuntu 默认带有的一个软件管理器。另外一个软件报管理器是 **apt**

## 问题

截止到 2022-08-01，**Ubuntu22.04** 默认带的 **firefox** 浏览器无法正常启动

> 其它版本没有测试过

在启动时，从 **开始菜单** 启动，没有反应。继续尝试在命令行启动，主要是看一下报错信息

在终端命令行键入命令 **firefox** 即可启动 **Firefox**

```
firefox
```

终端出现下面的报错

```
rosecoder@rosecoder:~$ firefox
update.go:85: cannot change mount namespace according to change mount (/var/lib/snapd/hostfs/usr/share/libreoffice/help /usr/share/libreoffice/help none bind,ro 0 0): cannot create directory "/usr/share/libreoffice/help": permission denied
Gtk-Message: 11:19:46.906: Failed to load module "canberra-gtk-module"
Gtk-Message: 11:19:46.985: Failed to load module "canberra-gtk-module"
ATTENTION: default value of option mesa_glthread overridden by environment.
ATTENTION: default value of option mesa_glthread overridden by environment.
ATTENTION: default value of option mesa_glthread overridden by environment.
```

具体的原因未知

## 解决方案

### 解决方案1

卸载以 **snap**  方式安装的 **fireofx**，重新通过其它途径下载 **Firefox**

````
sudo snap remove firefox
````

不使用包管理器来安装 **firefox**，在 firefox 的官网提供了 **tar.xz** 的安装方式，解压就可以直接使用

> 这个方式相对于使用 APT 来安装的确定是：版本更新必须手动更新

### 解决方案2

卸载以 **snap**  方式安装的 **fireofx**，并重新使用 **snap** 安装

卸载

```
sudo snap remove firefox
```

安装

```
sudo snap install firefox
```

## 注意

值得注意的是，在卸载使用  **snap** 不能使用 **APT** 来安装 **firefox**，

使用 **apt** 来安装，最后仍然会调用 **snap** 来安装

```
➜  ~ sudo apt install firefox 
正在读取软件包列表... 完成
正在分析软件包的依赖关系树... 完成
正在读取状态信息... 完成                 
下列【新】软件包将被安装：
  firefox
升级了 0 个软件包，新安装了 1 个软件包，要卸载 0 个软件包，有 167 个软件包未被升级。
需要下载 72.3 kB 的归档。
解压缩后会消耗 261 kB 的额外空间。
获取:1 http://mirrors.aliyun.com/ubuntu jammy/main amd64 firefox amd64 1:1snap1-0ubuntu2 [72.3 kB]
已下载 72.3 kB，耗时 0秒 (515 kB/s)
正在预设定软件包 ...
正在选中未选择的软件包 firefox。
(正在读取数据库 ... 系统当前共安装有 263603 个文件和目录。)
准备解压 .../firefox_1%3a1snap1-0ubuntu2_amd64.deb  ...
=> Installing the firefox snap
==> Checking connectivity with the snap store
==> Installing the firefox snap
firefox 103.0.2-1 已从 Mozilla✓ 安装
=> Snap installation complete
正在解压 firefox (1:1snap1-0ubuntu2) ...
正在设置 firefox (1:1snap1-0ubuntu2) ...
正在处理用于 mailcap (3.70+nmu1ubuntu1) 的触发器 ...
正在处理用于 desktop-file-utils (0.26-1ubuntu3) 的触发器 ...
正在处理用于 hicolor-icon-theme (0.17-2) 的触发器 ...
正在处理用于 gnome-menus (3.36.0-1ubuntu3) 的触发器 ...

```

这一点和安装 **chromium** 浏览器的情况一样

- [askubuntu](https://askubuntu.com/questions/1409575/ubuntu-22-04-lts-starting-firefox-through-terminal-error-cannot-change-mount)
