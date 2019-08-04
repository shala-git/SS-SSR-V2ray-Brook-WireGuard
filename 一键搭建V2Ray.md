## **1、V2Ray简介**

#### **什么是V2Ray**

Project V 提供了单一的内核和多种界面操作方式。内核（V2Ray）用于实际的网络交互、路由等针对网络数据的处理，而外围的用户界面程序提供了方便直接的操作流程，简单来说，V2Ray就是一个代理软件，可以用来科学上网学习国外先进科学技术。

#### **V2Ray与Shadowsocks区别**

V2Ray是在Shadowsocks的作者被请喝茶之后出现的一个开源项目，目的就是为了更好的科学上网。相比于ss，V2Ray的定位是一个平台，任何开发者都可以在这个平台上利用V2Ray开发出一个新的代理软件，简单来说，ss的定位比较简单，功能也比较单一，而V2Ray的功能非常强大，相对的，V2Ray的**配置就会复杂很多**，喜欢鼓捣的同学可以试试。

#### **V2Ray的优势**

> - **更完善的协议:** V2Ray 使用了新的自行研发的 VMess 协议，改正了 Shadowsocks 一些已有的缺点，更难被墙检测到（不保证可靠性）
> - **更强大的性能:** 网络性能更好，具体数据可以看 V2Ray 官方博客
> - **更丰富的功能:**
>
> 以下是部分 V2Ray 的功能
>
> - mKCP: KCP 协议在 V2Ray 上的实现，不必另行安装 kcptun
> - 动态端口：动态改变通信的端口，对抗对长时间大流量端口的限速封锁
> - 路由功能：可以随意设定指定数据包的流向，去广告、反跟踪都可以
> - 传出代理：看名字可能不太好理解，其实差不多可以称之为多重代理。类似于 Tor 的代理
> - 数据包伪装：类似于 Shadowsocks-rss 的混淆，另外对于 mKCP 的数据包也可伪装，伪装常见流量，令识别更困难
> - WebSocket 协议：可以 PaaS 平台搭建V2Ray，通过 WebSocket 代理。也可以通过它使用 CDN 中转，抗封锁效果更好
> - Mux:多路复用，进一步提高科学上网的并发性能

## 2、美国VPS Hostwinds 购买

首先确认不要使用任何代理，网络是什么 IP 就是什么 IP ，不然可能需要人工审核，导致 Hostwinds VPS 购买显示 "Pending" 状态， 不能即时创建服务激活。

1、通过[ Hostwinds 优惠链接进入](https://affiliates.hostwinds.com/hostwinds.php?id=7011&url=1224)Hostwinds 首页，选择 “VPS” 下的 "Unmanaged VPS" ，这里是最便宜的**(注意千万不要选择页面上 3.29 美元那个，那个是虚拟空间，不是 VPS !!!)**。

[![img](https://user-images.githubusercontent.com/52620310/62405902-216e0d00-b5d6-11e9-8361-a3a75797b52f.jpg)](https://user-images.githubusercontent.com/52620310/62405902-216e0d00-b5d6-11e9-8361-a3a75797b52f.jpg)

2、进入 VPS 选择页面后，根据自己的需要的配置选择套餐，一般我们选择最低配置就够用了，然后点击 “Order” 按钮进入信息填写页面，如下所示：

[![img](https://user-images.githubusercontent.com/52620310/62405905-27fc8480-b5d6-11e9-85d3-70c4f202ef17.jpg)](https://user-images.githubusercontent.com/52620310/62405905-27fc8480-b5d6-11e9-85d3-70c4f202ef17.jpg)

3、进入信息填写页面后首先填写账号信息，一般是新用户我们填写左边的姓、名、邮箱、密码，然后点击 “Submit” 进入下一步，如下图所示：

[![img](https://user-images.githubusercontent.com/52620310/62405907-2cc13880-b5d6-11e9-8dd3-bca5e119f97d.jpg)](https://user-images.githubusercontent.com/52620310/62405907-2cc13880-b5d6-11e9-8dd3-bca5e119f97d.jpg)

4、页面跳转后填写用户信息，如下图所示：

[![img](https://user-images.githubusercontent.com/52620310/62405909-321e8300-b5d6-11e9-8efc-d25563e38ea1.jpg)](https://user-images.githubusercontent.com/52620310/62405909-321e8300-b5d6-11e9-8efc-d25563e38ea1.jpg)

5、然后选择购买时间、数据中心 、操作系统，红色部分需要自己选择，绿色一般我们默认，可以按月购买，但是建议第一次购买时间选择长一点，这样优惠要大很多，不然后面续费优惠力度就没有这么大了。 如下图所示：

[![img](https://user-images.githubusercontent.com/52620310/62405910-36e33700-b5d6-11e9-916a-21611cae95ba.jpg)](https://user-images.githubusercontent.com/52620310/62405910-36e33700-b5d6-11e9-916a-21611cae95ba.jpg)

6、默认是自动云备份的，如果不需要去掉勾选， 如下图所示：

[![img](https://user-images.githubusercontent.com/52620310/62405913-3c408180-b5d6-11e9-908d-d475887eda70.jpg)](https://user-images.githubusercontent.com/52620310/62405913-3c408180-b5d6-11e9-908d-d475887eda70.jpg)

7、然后选择付款方式，一般我们选择支付宝进行付款 （只有国内 IP 访问的时候才有支付宝付款方式），如下图所示：

[![img](https://user-images.githubusercontent.com/52620310/62405915-406c9f00-b5d6-11e9-90d8-7eed10538637.jpg)](https://user-images.githubusercontent.com/52620310/62405915-406c9f00-b5d6-11e9-90d8-7eed10538637.jpg)

8、最后确认价格（不同时期可能价格有些许不同，如果通过前面优惠链接点击购买会有优惠），勾选同意协议，然后点击“Complete Order”按钮进行下单， 如下图所示：

[![img](https://user-images.githubusercontent.com/52620310/62405916-4498bc80-b5d6-11e9-8ecd-77d1f9587e94.jpg)](https://user-images.githubusercontent.com/52620310/62405916-4498bc80-b5d6-11e9-8ecd-77d1f9587e94.jpg)

9、下单完成后订单结果如下图所示：

[![img](https://user-images.githubusercontent.com/52620310/62405918-482c4380-b5d6-11e9-970d-4fce99d5d1e6.jpg)](https://user-images.githubusercontent.com/52620310/62405918-482c4380-b5d6-11e9-970d-4fce99d5d1e6.jpg)

## 3、远程连接Hostwinds VPS

首先你需要通过 SSH 连接 [Hostwinds](https://affiliates.hostwinds.com/hostwinds.php?id=7011&url=1216) 的 Linux VPS，连接 Linux VPS 需要使用 SSH 工具，这里推荐使用 Xshell 可以复制粘贴命令，Xshell 本身是需要付款的，作为中国人当然是使用 XX 版了，这里提供下载包如下所示：

Xshell 下载地址：<https://pan.baidu.com/s/1v7RCM0IjZGn_q5aWS1WXWg>，提取码: q3jw

下载后解压安装即可。

#### 使用 Xshell 连接 Linux VPS

1、打开 Xshell，点击左上角“文件”-“新建”，打开连接弹出库。

[![img](https://user-images.githubusercontent.com/52620310/62405920-537f6f00-b5d6-11e9-8665-b9ff1741d477.jpg)](https://user-images.githubusercontent.com/52620310/62405920-537f6f00-b5d6-11e9-8665-b9ff1741d477.jpg)

2、在 Xshell 弹出框中输入 IP 和端口，端口一般是 22 默认，然后点击确认按钮，如下图所示：

[![img](https://user-images.githubusercontent.com/52620310/62405922-567a5f80-b5d6-11e9-8b7a-2662799e0585.jpg)](https://user-images.githubusercontent.com/52620310/62405922-567a5f80-b5d6-11e9-8b7a-2662799e0585.jpg)

3、然后输入用户名 root，勾选记住用户名。

[![img](https://user-images.githubusercontent.com/52620310/62405925-5a0de680-b5d6-11e9-87bf-426f33dab264.jpg)](https://user-images.githubusercontent.com/52620310/62405925-5a0de680-b5d6-11e9-87bf-426f33dab264.jpg)

4、然后输入密码，勾选记住密码，点击确定。

[![img](https://user-images.githubusercontent.com/52620310/62405927-5e3a0400-b5d6-11e9-9b46-231b6b152909.jpg)](https://user-images.githubusercontent.com/52620310/62405927-5e3a0400-b5d6-11e9-9b46-231b6b152909.jpg)

完成以上步骤后就可以看到连接成功的界面，如下图所示：

[![img](https://user-images.githubusercontent.com/52620310/62405930-64c87b80-b5d6-11e9-9f01-3a5ab54e1dda.jpg)](https://user-images.githubusercontent.com/52620310/62405930-64c87b80-b5d6-11e9-9f01-3a5ab54e1dda.jpg)

## 4、一键脚本搭建V2Ray

在上图的待输入内容处，粘贴下面的命令（复制下面的命令，然后在 Xshell 待输入内容处“鼠标右键”/“粘贴”即可）：

```
# 安装wget
sudo yum -y install wget
# 下载脚本
wget https://install.direct/go.sh
# 安装unzip
sudo yum install zip unzip 
# 执行安装
sudo bash go.sh 
Installing V2Ray v3.14 on x86_64
Downloading V2Ray.
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   608    0   608    0     0   2229      0 --:--:-- --:--:-- --:--:--  2235
100 8482k  100 8482k    0     0  2501k      0  0:00:03  0:00:03 --:--:-- 2813k
Extracting V2Ray package to /tmp/v2ray.
Archive:  /tmp/v2ray/v2ray.zip
   creating: /tmp/v2ray/v2ray-v3.14-linux-64/
  inflating: /tmp/v2ray/v2ray-v3.14-linux-64/geoip.dat  
  inflating: /tmp/v2ray/v2ray-v3.14-linux-64/geosite.dat  
  inflating: /tmp/v2ray/v2ray-v3.14-linux-64/readme.md  
   creating: /tmp/v2ray/v2ray-v3.14-linux-64/systemd/
  inflating: /tmp/v2ray/v2ray-v3.14-linux-64/systemd/v2ray.service  
   creating: /tmp/v2ray/v2ray-v3.14-linux-64/systemv/
  inflating: /tmp/v2ray/v2ray-v3.14-linux-64/systemv/v2ray  
  inflating: /tmp/v2ray/v2ray-v3.14-linux-64/v2ctl  
 extracting: /tmp/v2ray/v2ray-v3.14-linux-64/v2ctl.sig  
  inflating: /tmp/v2ray/v2ray-v3.14-linux-64/v2ray  
 extracting: /tmp/v2ray/v2ray-v3.14-linux-64/v2ray.sig  
  inflating: /tmp/v2ray/v2ray-v3.14-linux-64/vpoint_socks_vmess.json  
  inflating: /tmp/v2ray/v2ray-v3.14-linux-64/vpoint_vmess_freedom.json  
PORT:13437
UUID:f500ecf5-e135-49c6-9ce2-78eb490d0aa9
Created symlink from /etc/systemd/system/multi-user.target.wants/v2ray.service to /etc/systemd/system/v2ray.service.
V2Ray v3.14 is installed.
```

在首次安装完成之后，V2Ray 不会自动启动，需要手动运行上述启动命令。而在已经运行 V2Ray 的 VPS 上再次执行安装脚本，安装脚本会自动停止 V2Ray 进程，升级 V2Ray 程序，然后自动运行 V2Ray。在升级过程中，配置文件不会被修改。

```
## 启动
sudo systemctl start v2ray

## 停止
sudo systemctl stop v2ray

## 重启
sudo systemctl restart v2ray
```

**配置**

如果你按照上面的命令执行安装完成之后，服务端其实是不需要再进行任何配置的，配置文件位于`/etc/v2ray/config.json`，使用`cat /etc/v2ray/config.json`查看配置信息。接下来进行客户端配置就行了。

**说明：**

- 配置文件中的 id、端口、alterId 需要和客户端的配置保持一致；
- 服务端使用脚本安装成功之后默认就是 vmess 协议；

配置完成之后重启 V2ray。

## 5、客户端配置

下载地址：[客户端](https://github.com/v2ray/v2ray-core/releases)

对`v2ray-windows-64.zip`进行解压，然后将下载的`V2RayN.exe`复制到解压后的目录，即两个下载好的文件需要在同一目录。

[![1](https://user-images.githubusercontent.com/52620310/62425495-3e592c00-b70d-11e9-8b49-2c9a8434d65c.jpg)](https://user-images.githubusercontent.com/52620310/62425495-3e592c00-b70d-11e9-8b49-2c9a8434d65c.jpg)

**配置**

运行 V2RayN.exe，然后进行配置。

客户端的配置需要根据你的服务端进行相应的配置，因为你的服务端协议可能是 vmess,shadowsocks 等。

如果你的服务端配置是协议 vmess，则配置如下：

[![2](https://user-images.githubusercontent.com/52620310/62425498-487b2a80-b70d-11e9-8b83-fa55071a144a.jpg)](https://user-images.githubusercontent.com/52620310/62425498-487b2a80-b70d-11e9-8b83-fa55071a144a.jpg)

[![3](https://user-images.githubusercontent.com/52620310/62425505-4e710b80-b70d-11e9-9919-c48da75516ac.jpg)](https://user-images.githubusercontent.com/52620310/62425505-4e710b80-b70d-11e9-9919-c48da75516ac.jpg)

[![4](https://user-images.githubusercontent.com/52620310/62425519-55981980-b70d-11e9-8f32-41a52e154fa8.jpg)](https://user-images.githubusercontent.com/52620310/62425519-55981980-b70d-11e9-8f32-41a52e154fa8.jpg)

## 6、Hostwinds 搭建 V2Ray 总结

以上就是美国 VPS Hostwinds 搭建 V2Ray 的教程，通过教可以轻松实现 Hostwinds 搭建 V2Ray，希望可以帮助需要使用 Hostwinds 搭建 V2Ray 的朋友。

[通过该优惠链接购买美国VPS Hostwinds](https://affiliates.hostwinds.com/hostwinds.php?id=7011&url=1216)，支持支付宝付款，欢迎购买注册。
