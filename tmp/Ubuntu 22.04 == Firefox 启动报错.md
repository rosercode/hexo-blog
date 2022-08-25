## 引言

**Firefox** 是 绝大多数 **Linux** 发行版的默认浏览器

**Ubuntu** 默认（内置）提供的浏览器也是 **Firefox**，从 Ubutnu21.10 之后的版本，默认是以 **snap** 的方式安装的。

> snap 是 Ubuntu 默认带有的一个软件管理器。另外一个软件报管理器是 **apt**

Ubuntu

## 问题

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

卸载以 **snap**  方式安装的 **fireofx**，重新通过其它途径下载 **Firefox**

````
sudo snap remove firefox
````

不使用包管理器来安装 **firefox**，在 firefox 的官网提供了 **tar.xz** 的安装方式，解压就可以直接使用

> 这个方式相对于使用 APT 来安装的确定是：版本更新必须手动更新

## 注意

值得注意的是，在卸载使用  **snap** 不能使用 **APT** 来安装 **firefox**，
