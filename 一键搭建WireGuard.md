## WireGuard简单介绍

> *注意：*WireGuard 是通过 **UDP** 协议传输数据的，这意味着它可以搭建在被墙的服务器上使用，**复活被墙IP**！
>
> *同时：*因为是 UDP 传输的，所以也**不怕被墙**，锐速、BBR 这类TCP加速工具也不会对其起到加速作用。
>
> *另外：*如果你**当地运营商对海外 UDP 链接进行 QOS 限速**，那么速度可能不如使用 TCP 链接的代理软件理想。

#### 更少的代码

相比于 OpenVPN 、 IPSec 的几十万行代码，WireGuard 只有短短的四千行。

#### 更容易部署

对于初次接触的人来说，相比于其他VPN协议，WireGuard 更容易部署。

#### 更安全的加密

- Curve25519 目前最高水平的秘钥交换算法。
- ChaCha20 对称加解密算法，比 AES 更快更高效。
- Poly1305 是一种 MAC (Message Authentication Code) 标准，用于验证数据的完整性和消息的真实性。
- BLAKE2 一种更安全的 HASH 算法（类似的有 SHA1, SHA256, MD5）
- SipHash24 另一种 HASH 算法。
- HKDF 一种秘钥衍生算法。

因为其链接特性，所以 WireGuard 有很好的稳定性，无论你怎么切换网络 或者 网络波动导致断开后，往往可以很快恢复链接，所以如果拿来加速游戏的话，可能效果不错(当然前提是你的代理服务器也要网络不错)。



## 前提要求

- **系统要求：**Debian 8 / 9、Ubuntu 14.04 / 16.04 / 18.04 / 18.10
- **服务器要求：**OpenVZ 虚拟化的服务器不支持安装该VPN，其他虚拟化均可。这里我推荐使用Vultr VPS主机，注册购买教程如下：

#### [Vultr VPS](https://www.vultr.com/?ref=8169051-4F)主机官网账户注册

Vultr 官网账户注册，我们打开官网后输入邮箱和密码进行点击 Create Account 进行账户创建！限时活动，**通过文中链接注册并在 30 天内充值  25美金可获赠 50 美金额度**。

访问 Vultr 活动官网地址：[Vultr活动官网](https://www.vultr.com/?ref=8169051-4F)

[![1](https://user-images.githubusercontent.com/52620310/62409248-0a93de80-b607-11e9-9da8-99182bb51016.png)](https://user-images.githubusercontent.com/52620310/62409248-0a93de80-b607-11e9-9da8-99182bb51016.png)

##### **账户注册注意问题**

账户注册密码要求至少十位，而且必须至少包含一个大写字母、一个小写字母和一个数字，如果提示注册成功需要邮箱验证的话，请到注册邮箱查看邮件并点击 Verify Your E-mail 验证邮箱（收件箱如果没有收到，查看下垃圾箱）！

[![2](https://user-images.githubusercontent.com/52620310/62409253-11baec80-b607-11e9-8e85-7eb324fefa60.png)](https://user-images.githubusercontent.com/52620310/62409253-11baec80-b607-11e9-8e85-7eb324fefa60.png)

#### 2. Vultr 账户充值

我们将 Vultr 账户注册好之后登录到 Vultr 官网后台景象账户充值。目前 Vultr 支持信用卡（Credit Card）、PayPal、比特币（Bitcoin）、支付宝（Alipay）和微信支付（WeChat Pay）五种付款方式。我们可以选择常用的支付宝和微信来进行充值即可。我们选择支付宝付款，确定首次充值额度（**最低 10 美金**），并且勾选同意条款后，点击按钮 **Pay with Alipay** 即可。

***PS：**如果我们有优惠码的话还可以在 Enter Code 输入优惠码并点击 Apply 进行应用，目前暂无官方优惠码！*

[![3](https://user-images.githubusercontent.com/52620310/62409255-167fa080-b607-11e9-9117-bfb89b19d4fd.png)](https://user-images.githubusercontent.com/52620310/62409255-167fa080-b607-11e9-9117-bfb89b19d4fd.png)

我们稍等片刻后便会跳转到我们熟悉的支付宝付款页面，直接扫一扫或者登录账户付款就可以了，我们付款成功后可以在 Vultr 后台查看余额。

***PS：**为防止滥用账号重复申请，Vultr 会检测支付帐号，如果使用了同一个 PayPal 或信用卡去支付，会被 vultr 封号。*

![](https://user-images.githubusercontent.com/52620310/62409256-1aabbe00-b607-11e9-8a10-33a1da5f4251.png)

#### 3.Vultr 创建服务器

我们将左侧栏菜单切换到 Servers 进行服务器创建，我们首先选择服务器机房位置地址。这里我们搭建 SS 或 SSR 的话推荐日本东京（Tokyo，Japan）和美国洛杉矶（Los Angeles，United States）。

![](https://user-images.githubusercontent.com/52620310/62409258-1e3f4500-b607-11e9-8566-7712ed814588.png)

Vultr VPS 主机操作系统我们选择 Ubuntu。

![](https://user-images.githubusercontent.com/52620310/62474576-c3a81380-b7d5-11e9-9463-4279dec0952c.png)

我们选择 Vultr 套餐计划，套餐计划的最低价格根据主机位置的不同而不同，目前选择的日本东京最低套餐计划每月 5 美元，每小时 0.007 美元，配置是 1 个 CPU，1G 内存和 1000GB 流量。这个最低套餐计划完全可以满足我们个人需要了。

[![6](https://user-images.githubusercontent.com/52620310/62409262-26978000-b607-11e9-961e-375ef9c7e782.png)](https://user-images.githubusercontent.com/52620310/62409262-26978000-b607-11e9-961e-375ef9c7e782.png)

***PS：****我们根据自己的需求去选择相应的 VPS 主机配置，Vultr 采用小时计费，如果我们不想继续使用或创建新的 VPS 的时候，可以销毁多余的 VPS，扣除的费用是已使用小时数乘以小时单价，而不是按月扣费！*

我们如果对 IPv6 有需求的话可以勾选一下，其余的就保持默认就可以了，配置完成后我们直接点击 **Deploy Now** 进行 VPS 部署。

[![7](https://user-images.githubusercontent.com/52620310/62409265-2b5c3400-b607-11e9-950f-766539fe587e.png)](https://user-images.githubusercontent.com/52620310/62409265-2b5c3400-b607-11e9-950f-766539fe587e.png)

我们大约等待一分钟后就可以成功部署，当显示 **Running** 时，就表示部署已完成。之后你可以随时停用、重启或销毁它。

[![8](https://user-images.githubusercontent.com/52620310/62409267-2f885180-b607-11e9-9b16-cb89e92448ee.png)](https://user-images.githubusercontent.com/52620310/62409267-2f885180-b607-11e9-9b16-cb89e92448ee.png)

我们将 VPS 部署成功后就可以看到服务器的基本信息：ROOT 密码、IP 地址、内存、硬盘和带宽等相关信息，这样我们就成功部署了 VPS，接下来就要进行 WireGuard 的搭建了。

![9](https://user-images.githubusercontent.com/52620310/62409268-331bd880-b607-11e9-90cc-a0b2b1da7188.png)

> *注意：*如果你用的也是 Vultr，且你本地没有 IPv6 地址，那就不要勾选 **Enable IPv6** ，否则可能客户端链接时可能会出错。

**另外，请确保你的系统是纯净的，建议重装系统后直接开始本教程！**



## WireGuard安装步骤

#### 配置PPA

首先如果你是 Ubuntu 14.04 系统，那么请先安装 PPA：

```
# 以下步骤仅限 Ubuntu 14.04 系统执行
apt update
apt install software-properties-common -y
```

安装完成后，我们还需要通过 PPA 工具添加 WireGuard 源：

```
add-apt-repository ppa:wireguard/wireguard
# 执行后提示如下示例内容（仅供参考）：
 
root@doubi:~# add-apt-repository ppa:wireguard/wireguard
 WireGuard is a novel VPN that runs inside the Linux Kernel. This is the Ubuntu packaging for WireGuard. More info may be found at its website, listed below.
 
More info: https://www.wireguard.com/
Packages: wireguard wireguard-tools wireguard-dkms
 
Install with: $ apt install wireguard
 
For help, please contact 
 More info: https://launchpad.net/~wireguard/+archive/ubuntu/wireguard
Press [ENTER] to continue or ctrl-c to cancel adding it
 
# 这里会提示你是否继续，点击 回车键 继续，点击 Ctrl+C 键退出。
# 然后输出大概如下内容。
 
gpg: keyring '/tmp/tmp8bgitjjx/secring.gpg' created
gpg: keyring '/tmp/tmp8bgitjjx/pubring.gpg' created
gpg: requesting key 504A1A25 from hkp server keyserver.ubuntu.com
gpg: /tmp/tmp8bgitjjx/trustdb.gpg: trustdb created
gpg: key 504A1A25: public key "Launchpad PPA for wireguard-ppa" imported
gpg: Total number processed: 1
gpg:               imported: 1  (RSA: 1)
OK
 
# 以上为输出示例内容（仅供参考）
```

#### 安装WireGuard

然后我们就可以开始安装 WireGuard 了。

```
# 更新一下软件包源
apt update
 
# 开始安装 WireGuard ，resolvconf 是用来指定DNS的，旧一些的系统可能没装。
apt install wireguard resolvconf -y
```



## 验证是否安装成功

当你通过上面的步骤安装完后，请用下面的代码验证一下是否安装成功。

```
lsmod | grep wireguard
# 执行该代码后，提示大概如下示例内容（仅供参考），第一行是必须要有的，至于下面的两行不同系统似乎还不一样，但是不影响使用。
 
root@doubi:~# modprobe wireguard && lsmod | grep wireguard
wireguard             212992  0
ip6_udp_tunnel         16384  1 wireguard
udp_tunnel             16384  1 wireguard
```



## 配置步骤

#### 生成密匙对

当你确定安装成功后，就要开始配置服务端和客户端的配置文件了。放心，这很简单。

```
# 首先进入配置文件目录，如果该目录不存在请先手动创建：mkdir /etc/wireguard
cd /etc/wireguard
 
# 然后开始生成 密匙对(公匙+私匙)。
wg genkey | tee sprivatekey | wg pubkey > spublickey
wg genkey | tee cprivatekey | wg pubkey > cpublickey
```

------

#### 查看主网卡名称

先查看一下你的主网卡名是什么：

```
ip addr
# 执行命令后，示例如下（仅供参考），lo 是本地环回 忽略，eth0 就是主网卡名了。
# 写着你的服务器外网IP的(下面 X.X.X.X 处)，就是你的主网卡，NAT的服务器则是显示内网IP。
# 如果你拿不准哪个网卡是主网卡，请留言询问。
 
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 00:16:3c:cf:89:73 brd ff:ff:ff:ff:ff:ff
    inet X.X.X.X/25 brd 255.255.255.255 scope global eth0
       valid_lft forever preferred_lft forever
```

------

#### 生成服务端配置文件

接下来就开始生成服务端配置文件：

```
# 井号开头的是注释说明，用该命令执行后会自动过滤注释文字。
# 下面加粗的这一大段都是一个代码！请把下面几行全部复制，然后粘贴到 SSH软件中执行，不要一行一行执行！
 
echo "[Interface]
# 服务器的私匙，对应客户端配置中的公匙（自动读取上面刚刚生成的密匙内容）
PrivateKey = $(cat sprivatekey)
# 本机的内网IP地址，一般默认即可，除非和你服务器或客户端设备本地网段冲突
Address = 10.0.0.1/24 
# 运行 WireGuard 时要执行的 iptables 防火墙规则，用于打开NAT转发之类的。
# 如果你的服务器主网卡名称不是 eth0 ，那么请修改下面防火墙规则中最后的 eth0 为你的主网卡名称。
PostUp   = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -A FORWARD -o wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
# 停止 WireGuard 时要执行的 iptables 防火墙规则，用于关闭NAT转发之类的。
# 如果你的服务器主网卡名称不是 eth0 ，那么请修改下面防火墙规则中最后的 eth0 为你的主网卡名称。
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -D FORWARD -o wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE
# 服务端监听端口，可以自行修改
ListenPort = 443
# 服务端请求域名解析 DNS
DNS = 8.8.8.8
# 保持默认
MTU = 1420
# [Peer] 代表客户端配置，每增加一段 [Peer] 就是增加一个客户端账号，具体我稍后会写多用户教程。
[Peer]
# 该客户端账号的公匙，对应客户端配置中的私匙（自动读取上面刚刚生成的密匙内容）
PublicKey = $(cat cpublickey)
# 该客户端账号的内网IP地址
AllowedIPs = 10.0.0.2/32"|sed '/^#/d;/^\s*$/d' > wg0.conf
 
# 上面加粗的这一大段都是一个代码！请把下面几行全部复制，然后粘贴到 SSH软件中执行，不要一行一行执行！
```

#### 生成客户端配置文件

接下来就开始生成客户端配置文件：

```
# 井号开头的是注释说明，用该命令执行后会自动过滤注释文字。
# 下面加粗的这一大段都是一个代码！请把下面几行全部复制，然后粘贴到 SSH软件中执行，不要一行一行执行！
 
echo "[Interface]
# 客户端的私匙，对应服务器配置中的客户端公匙（自动读取上面刚刚生成的密匙内容）
PrivateKey = $(cat cprivatekey)
# 客户端的内网IP地址
Address = 10.0.0.2/24
# 解析域名用的DNS
DNS = 8.8.8.8
# 保持默认
MTU = 1420
[Peer]
# 服务器的公匙，对应服务器的私匙（自动读取上面刚刚生成的密匙内容）
PublicKey = $(cat spublickey)
# 服务器地址和端口，下面的 X.X.X.X 记得更换为你的服务器公网IP，端口请填写服务端配置时的监听端口
Endpoint = X.X.X.X:443
# 因为是客户端，所以这个设置为全部IP段即可
AllowedIPs = 0.0.0.0/0, ::0/0
# 保持连接，如果客户端或服务端是 NAT 网络(比如国内大多数家庭宽带没有公网IP，都是NAT)，那么就需要添加这个参数定时链接服务端(单位：秒)，如果你的服务器和你本地都不是 NAT 网络，那么建议不使用该参数（设置为0，或客户端配置文件中删除这行）
PersistentKeepalive = 25"|sed '/^#/d;/^\s*$/d' > client.conf
 
# 上面加粗的这一大段都是一个代码！请把下面几行全部复制，然后粘贴到 SSH软件中执行，不要一行一行执行！
```

接下来你就可以将这个客户端配置文件 **[/etc/wireguard/client.conf]** 通过SFTP、HTTP等方式下载到本地了。

不过我更推荐，SSH中打开显示配置文件内容并复制出来后，本地设备新建一个文本文件 **[xxx.conf] (名称随意，后缀名需要是 .conf)** 并写入其中，提供给 WireGuard 客户端读取使用。

```
cat /etc/wireguard/client.conf
```

#### 其他剩余其他操作：

```
# 赋予配置文件夹权限chmod 777 -R /etc/wireguard # 打开防火墙转发功能echo 1 > /proc/sys/net/ipv4/ip_forwardecho "net.ipv4.ip_forward = 1" >> /etc/sysctl.confsysctl -p
```



## 启动WireGuard

```
wg-quick up wg0
# 执行命令后，输出示例如下（仅供参考）
 
[#] ip link add wg0 type wireguard
[#] wg setconf wg0 /dev/fd/63
[#] ip address add 10.0.0.1/24 dev wg0
[#] ip link set mtu 1420 dev wg0
[#] ip link set wg0 up
[#] resolvconf -a tun.wg0 -m 0 -x
[#] iptables -A FORWARD -i wg0 -j ACCEPT; iptables -A FORWARD -o wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
 
# 如果此处没有报错：RTNETLINK answers: Operation not supported，且输入内容差不多，那么说明启动成功了！
```

------

### 停止WireGuard

```
wg-quick down wg0
```

------

### 查询WireGuard状态

```
wg
```

------

### 开机启动

> *注意：*Ubuntu 14.04 系统默认是没有 systemctl 的，所以无法配置开机启动。

```
# 设置开机启动
systemctl enable wg-quick@wg0
# 取消开机启动
systemctl disable wg-quick@wg0
```



## 总结

以上就是美国 VPS Vultr 一键搭建 WireGuard 的教程，通过该教程可以轻松实现 Vultr 搭建 WireGuard，希望可以帮助需要使用 Vultr VPS 搭建 WireGuard 的朋友。

[**通过本链接注册并在 30 天内充值 25 美金可获赠 50 美金额度**](https://www.vultr.com/?ref=8169051-4F)，支持支付宝付款，欢迎购买注册。

