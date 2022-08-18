## 引言

Linux netstat 命令用于显示网络状态。

利用 netstat 指令可让你得知整个 Linux 系统的网络情况。 

- 注意：部分 Linux 发行部不带有这个命令，需要安装 **net-tools** 包
- 注意：Windows 也带有 **netstat** 这个命令，作用相同，但是参数完全不同

## 参数

```
-a或--all 显示所有连线中的Socket。
-A<网络类型>或--<网络类型> 列出该网络类型连线中的相关地址。
-c或--continuous 持续列出网络状态。
-C或--cache 显示路由器配置的快取信息。
-e或--extend 显示网络其他相关信息。
-F或--fib 显示路由缓存。
-g或--groups 显示多重广播功能群组组员名单。
-h或--help 在线帮助。
-i或--interfaces 显示网络界面信息表单。
-l或--listening 显示监控中的服务器的Socket。
-M或--masquerade 显示伪装的网络连线。
-n或--numeric 直接使用IP地址，而不通过域名服务器。
-N或--netlink或--symbolic 显示网络硬件外围设备的符号连接名称。
-o或--timers 显示计时器。
-p或--programs 显示正在使用Socket的程序识别码和程序名称。
-r或--route 显示Routing Table。
-s或--statistics 显示网络工作信息统计表。
-t或--tcp 显示TCP传输协议的连线状况。
-u或--udp 显示UDP传输协议的连线状况。
-v或--verbose 显示指令执行过程。
-V或--version 显示版本信息。
-w或--raw 显示RAW传输协议的连线状况。
-x或--unix 此参数的效果和指定"-A unix"参数相同。
--ip或--inet 此参数的效果和指定"-A inet"参数相同。
```

## 常用实例

```
admin@iZuf6j4r8gknclj8rxdavcZ: $ netstat -ant
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21              0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:888             0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21115           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21116           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21117           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21118           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21119           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:3307            0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.1:587           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:6379            0.0.0.0:*               LISTEN     
tcp        0      0 172.17.28.21:21118      94.102.49.57:65486      ESTABLISHED
tcp        0      0 172.17.28.21:8888       89.248.163.246:50485    ESTABLISHED
tcp        0      0 172.17.28.21:22         117.83.134.28:45148     ESTABLISHED
tcp        0      0 172.17.28.21:53172      104.16.19.35:443        ESTABLISHED
tcp        1      0 172.17.28.21:8888       47.100.57.211:56508     CLOSE_WAIT 
tcp        0      0 172.17.28.21:50474      100.100.109.104:80      TIME_WAIT  
tcp        0      0 172.17.28.21:57350      100.100.36.108:443      TIME_WAIT  
tcp        0    316 172.17.28.21:22         117.83.134.28:45152     ESTABLISHED
tcp        0      0 172.17.28.21:35230      100.100.30.26:80        ESTABLISHED
tcp6       0      0 :::22222                :::*                    LISTEN     
tcp6       0      0 127.0.0.1:8081          :::*                    LISTEN     
tcp6       0      0 :::21                   :::*                    LISTEN     
tcp6       0      0 :::7000                 :::*                    LISTEN     
tcp6       0      0 :::8443                 :::*                    LISTEN     
tcp6       0      0 :::8232                 :::*                    LISTEN     
tcp6       0      0 :::9801                 :::*                    LISTEN     
tcp6       0      0 :::29418                :::*                    LISTEN     
tcp6       0      0 :::9418                 :::*                    LISTEN     
```

实例依次是 

查看正在监听的端口

```
admin@iZuf6j4r8gknclj8rxdavcZ: $ netstat -ant | grep 'LISTEN'
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:888             0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.1:25            0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21115           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21116           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21117           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21118           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:21119           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:3307            0.0.0.0:*               LISTEN     
tcp        0      0 127.0.0.1:587           0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:6379            0.0.0.0:*               LISTEN     
tcp6       0      0 :::22222                :::*                    LISTEN     
tcp6       0      0 127.0.0.1:8081          :::*                    LISTEN     
tcp6       0      0 :::7000                 :::*                    LISTEN     
tcp6       0      0 :::8443                 :::*                    LISTEN     
tcp6       0      0 :::8232                 :::*                    LISTEN     
tcp6       0      0 :::9801                 :::*                    LISTEN     
tcp6       0      0 :::29418                :::*                    LISTEN     
tcp6       0      0 :::9418                 :::*                    LISTEN     
tcp6       0      0 :::3306                 :::*                    LISTEN     
tcp6       0      0 :::3307                 :::*                    LISTEN     
tcp6       0      0 ::1:6379                :::*                    LISTEN  
```

