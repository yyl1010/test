# adb命令

###### ADB 全称为 Android Debug Bridge，起到调试桥的作用，是一个客户端-服务器端程序。其中客户端是用来操作的电脑，服务端是 Android 设备。

###### ADB 也是 Android SDK 中的一个工具，可以直接操作管理 Android 模拟器或者真实的 Android 设备。

## 1.adb作用

###### 运行设备的 shell(命令行)，管理模拟器或设备的端口映射，计算机和设备之间上传/下载文件，可以对设备的应用进行卸载安装等，在 App 遇到 ANR/Crash 等 bug 时，可以通过 ADB 来抓取日志

###### 简而言之，ADB 就是连接 Android 手机与 PC 端的桥梁，所以ADB又称为安卓调试桥（注意：是安卓，不是iOS），可以让用户在电脑上对手机进行全面的操作！

##### 准备工作：

###### 下载adb-将路径放到path环境变量中-命令行输入adb测试是否安装好

##### **连接**手机：

###### 可以通过模拟器连接，也可以通过数据线连接。

###### 通过数据线连接时，手机进入“开发者选项”，打开“usb调试”。（不同品牌安卓机型，首次打开“开发者选项”方式不一样，大多是双击手机版本号3~5次，会toast提醒“开发者模式已打开”，具体打开方式可根据手机品牌进行百度查询）

### 2.**基本命令**

> adb version ：显示 adb 版本

1. **adb help：帮助信息，查看adb所支持的所有命令**
2. **adb devices：查看当前连接的设备，已连接的设备会显示出来**
3. **adb get-serialno：也可以查看设备号**

### 3.**权限命令**

**adb root：获取Android管理员（root用户）的权限。**

**注意**：一般测试机可使用root权限。

Android版本9以上，不支持商用机使用root权限，但可以修改底层一些配置

**adb shell：登录设备 shell，该命令将登录设备的shell（内核），登录shell后，可以使用 cd，ls，rm 等Linux命令**

### 4.**建立连接**

**adb -d：如果同时连了usb，又开了模拟器，连接当前唯一通过usb连接的安卓设备**

**adb -e shell：指定当前连接此电脑的唯一的一个模拟器**

**adb -s <设备号> shell：当电脑插多台手机或模拟器时，指定一个设备号进行连接**

**exit：退出**

**adb kill-server：杀死当前adb服务，如果连不上设备时，杀掉重启。（没事不要用它）**

**adb start-server：杀掉后重启**

**adb -p 6666 start-server：任意指定一个 adb shell 的端口**

**5037：adb默认端口，如果该端口被占用，可以指定一个端口号**

### 5.**apk 操作指令**

###### adb shell是进行安卓系统下操作，是在客户端也就是电脑端加些前缀，如果 是安卓端不用

1. **adb shell pm list packages：列出当前设备/手机，所有的包名**

2. **adb shell pm list packages -f：显示包和包相关联的文件(安装路径)**

3. **adb install <文件路径\apk>：将本地的apk软件安装到设备(手机)上。如手机外部安装需要密码，记得手机输入密码**

4. **adb install -r <文件路径\apk>：覆盖安装**

5. **adb uninstall <包名>：卸载该软件/app。注意：安装时安装的是apk，卸载时是包名，可以通过 adb shell pm list packages 查看需要卸载的包名。**

6. ##### adb shell dumpsys activity services [包名]： 查看正在运行的 Services

7. ##### adb shell dumpsys activity activities | grep mFocusedActivity ：查看前台 Activity

- adb shell pm list packages -d：显示禁用的包名

- adb shell pm list packages -e：显示当前启用的包名

- ##### adb shell pm list packages -s：显示系统应用包名

- ##### adb shell pm list packages -3：显示已安装第三方的包名

- adb shell pm list packages xxxx：加需要过滤的包名，如：xxx = taobao

- adb install -d <文件路径\apk>：允许降级覆盖安装

- adb install -g <文件路径\apk>：授权/获取权限，安装软件时把所有权限都打开
- adb shell pm uninstall -k <包名>：虽然把此应用卸载，但仍保存此应用的数据和缓存
- adb shell am force-stop <包名>：强制退出该应用/ap

### 6.文件操作指令

1. **adb push <本地pc路径\文件或文件夹> <手机端路径>：把本地(pc机)的文件或文件夹复制到设备(手机)**
2. **adb pull <手机端路径/文件或文件夹> <pc机路径>：把设备(手机)的文件或文件夹复制到本地。**

- 注意点1：pc机路径与Android机路径，分隔符是不同的。

- 注意点2：复制失败，大概率是无权限。可先使用上面介绍过的两个命令：adb root；adb remount。在使用 adb push 命令


### 7.日志操作指令

###### 日志的级别：E-error I-infomation D-debug W-warning

1. ##### adb logcat -d:将日志显示在控制台

2. ##### adb logcat > file-path:将日志输出到文件



#### 8.使用 Monkey 进行压力测试

###### Monkey 可以生成伪随机用户事件来模拟单击、触摸、手势等操作，可以对正在开发中的程序进行随机压力测试。

1. ##### adb shell monkey -p <packagename/包名> -v 500 ：表示向 `<packagename>` 指定的应用程序发送 500 个伪随机事件。

2. ##### *adb* shell monkey -p com.feicuiedu.monkeytestdemo -s 1476474162566 -v 1000 ：根据seed值（-s）来完成*bug*的复现