## How to cross-compile for BlackBerry 10
=========================================

>This guide will show you how to compile libraries for BlackBerry 10 and use it in you cascades project.

### Requirments

1. BlackBerry Momentics and at least ONE SDK installed.
2. Python or other tools required by specified project.
3. Some handy text editor, I'm using [visual Studio Code]()

### Example

>I'm taking Botan-1.10.17 as an example, it's the latest version which is good enough for qt4.

#### Device package 

Botan-1.10.17 ships with a ```configure.py``` to generate Makefile, read this file and go with this:

```
configure.py --cc=gcc --os=qnx --cpu=arm --cc-bin=arm-unknown-nto-qnx8.0.0eabi-gcc.exe --no-autoload --enable-modules=md5,camellia,cbc,cfb,crc32,des,rc2,rc5,rc6
```

You can view all the supported modules by use ```--no-autoload``` parameter only.

Now open the generated ```Makefile``` , change items below:
```
CXX  = qcc -V4.6.3,gcc_ntoarmv7le_cpp
AR   = arm-unknown-nto-qnx8.0.0eabi-ar crs
```
Then add some options:
```
#BLACKBERRY10
AS = qcc -V4.6.3,gcc_ntoarmv7le_cpp
CC = qcc -V4.6.3,gcc_ntoarmv7le
CPUVARDIR = armle-v7
LD = qcc -V4.6.3,gcc_ntoarmv7le_cpp
QCC_CONF_PATH = D:/dev/bbndk/host_10_3_1_12/win32/x86/etc/qcc/gcc
QNX_HOST = D:/dev/bbndk/host_10_3_1_12/win32/x86
QNX_TARGET = D:/dev/bbndk/target_10_3_1_995/qnx6
```
#Please change the path with your actual path#

Now open terminal here, type ```make``` to build this library for Device mode, this will generates a ```libbotan-1.10.so``` file, rename it to ```libbotan-1.10-device.so```

#### Simulator package

Momentics requires a simulator build when you try to add a third party library, for debug usage of course.

Modify Makefile items below :
```
CXX = qcc -V4.6.3,gcc_ntox86_cpp
AR  = arm-unknown-nto-qnx8.0.0eabi-ar crs
#BLACKBERRY10
AS = qcc -V4.6.3,gcc_ntox86_cpp
CC = qcc -V4.6.3,gcc_ntox86
CPUVARDIR = x86
LD = qcc -V4.6.3,gcc_ntox86_cpp
QCC_CONF_PATH = D:/dev/bbndk/host_10_3_1_12/win32/x86/etc/qcc/gcc
QNX_HOST = D:/dev/bbndk/host_10_3_1_12/win32/x86
QNX_TARGET = D:/dev/bbndk/target_10_3_1_995/qnx6
```

Change the path to your actual path instead.

Now open terminal here, type ```make``` to build this library for Simulator mode, this will generates a ```libbotan-1.10.so``` file, rename it to ```libbotan-1.10-simulator.so```


#### Use it in Momentics

Right-click your project, select configure / add library , add an External Library , specify the libbotan-1.10-release.so / libbotan-1.10-simulator.so , then add the include folder ( look for it in the ```build``` folder ). done.
