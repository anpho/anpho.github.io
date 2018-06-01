## Android Captive Portal Fix Guide

>去除Android 5.0 / 6.0原生系统上面的网络连接感叹号的一个方法。

### 为什么会出现叹号？

Android系统为了确认网络连接的有效性，会尝试与google的一台服务器进行通讯，有以下几种情况：

1.如果通讯成功，那么就说明当前网络连接是有效的互联网连接
1.如果总是被重定向到一个网页，说明你连接的是一个需要登录的wifi，比如电信、移动的公共wifi
1.如果完全没有响应，说明此网不通

然而在大陆，google的服务器是被屏蔽的，所以一直是 2 或者 3 的状态。

### 出现叹号会有什么影响？

网络连接出现叹号后，手机对网络连通性的判断就没有意义了，会导致的问题有： wifi自动断线（不在没有网络连接的连接上浪费时间）， wifi经常跳到手机网络（wlan状况不好时自动切换到运营商网络）等等。网上有禁掉这个captivePortal功能的方法，只是禁掉后网络连通性的判断功能也就完全失效，对于一些需要登录的wlan就不能判定了。

### 如何处理？

手机开usb调试后，在电脑上使用以下代码进行切换（将portal检测网址切换到anpho.github.io）：

```adb shell settings put global captive_portal_server anpho.github.io```

然后重启手机生效。

如果手机上安装有终端，也可以试试直接在终端里输入：

```settings put global captive_portal_server anpho.github.io```

的方式进行设置，设置完后重启手机生效。

[返回主页](https://anpho.github.io)
