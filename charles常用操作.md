# charles常用操作

#### charles安装证书抓取https请求-windows端

help-SSL Proxying-Install Charles Root Certificate
安装证书-本地计算机-下一步-将所有证书存放下列存储-浏览-受信任的根证书颁发机构-确定

1. cmd-ipconfig查看本机ip或charle中-help-local ip address

2. Proxy-Proxy Setting 设置端口号 默认8888，不要和其他程序冲突即可，并勾选Enable transparent HTTP proxying

3. Charles设置Proxy代理
   Proxy -> SSL Proxying Settings... 勾选Enable SSL Proxying,点击Add,点击Add，Host设置要抓取的https接口，  

   Host : * (使用通配符表示检测所有网络请求；Port：443）

   完成以上操作，就完成Charles抓取HTTP(S)数据包的所有配置了。

#### 抓取安卓http

在手机设备、模拟器或者远程浏览器上设置代理，抓取手机设备上的请求包（手机和电脑必须在同一个局域网内，并关闭电脑防火墙、其他代理或者翻墙软件）

1. 在手机wifi 上设置代理 -> 长按无线网络-->修改网络-->高级选项-->代理 手动-->手动输入输入IP、端口号（服务器IP：PC机器的IP  通过之前介绍的查看IP的方法）
2. Charles弹出询问“allow”或者“deny”,点击“allow”按钮允许；出现手机的HTTP请求列表，如果修改相关配置后，没有出现信息，可在设置中加入自己手机的IP：Proxy-Access Control Settings--add自己手机ip
3. 安装证书:抓取https数据需要在手机上安装证书，HTTPS的抓包需要在HTTP抓包基础上再进行设置：Help -> SSL proxying -> Install charles root certificate on a Mobile Device or remote browser…
4. 出现弹窗得到地址chls.pro/ssl

5. 在手机自带的系统浏览器输入地址chls.pro/ssl，出现证书安装页面，点击安装，手机设置有密码的输入密码进行安装。安装完证书后，就可以截取手机上的 Https 通讯内容了。不过同样需要注意，默认情况下 Charles 并不做截取，你还需要在要截取的网络请求上右击，选择 SSL proxy 菜单项。
   




#### charles弱网测试

 proxy-Throttle Settings-勾选Enable Throttling：在这里选择要模拟的网络环境,也可以自定义指定的url进行网络环境（勾选only....），通过该功能，模拟不同的网络带宽、延时率、丢包率。

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAxOS93ZWJwLzIwNjQ3MS8xNTY2MTMxMzc0MDU1LTg0ZTI5ZWZjLThmMzEtNGFkZi1iMWU0LTNiMDRkMTUyZWNhZC53ZWJw?x-oss-process=image/format,png)

![image.png](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAxOS9wbmcvMjA2NDcxLzE1Njc2NzA4MDQxMDgtZGE3ZDZlZTYtNzU2My00MDY1LThjOTMtYjE5MTZjYzZiOTA4LnBuZw?x-oss-process=image/format,png)



#### Charles断点测试

右击要打断点的接口-Breakpoints-浏览器刷新对应接口页面-自动跳动到charles-点击edit request修改请求信息-点击Edit Response-选择合适显示格式，比如json-修改对应数据-Execute-回到浏览器查看修改后的response响应信息-响应数据也可更改同样步骤



##### 设置代理后，浏览器打不开网页

浏览器--设置--打开代理设置--局域网设置--去除代理服务器下图选项后-确定

![img](https://imgconvert.csdnimg.cn/aHR0cHM6Ly9jZG4ubmxhcmsuY29tL3l1cXVlLzAvMjAxOS9wbmcvMjA2NDcxLzE1NjcwNTE0OTc4MDAtOWQzODE1ZGEtODQyOC00MmE0LWExN2UtOWRhNDQ1ZTJiNmQ0LnBuZw?x-oss-process=image/format,png)

#### Charles 简单的给服务器进行压力测试；

在进行压力测试的请求会话上右击，选择【Repeat Advanced】在弹出框中，输入并发线程数以及压力次数点击进行测试
