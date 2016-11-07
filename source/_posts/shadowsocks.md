title: Shadowsocks, a powerful tool you will need
tags: ["tools"]
date: 2015-02-05 3:18:12
---

# Why shadowsocks?
You know the reason Y shadowsocks. so, Let's get started:
But FYI, here the [Offical Site](http://shadowsocks.org/en/index.html) and [Source](https://github.com/shadowsocks/shadowsocks)

<!-- more -->

## VPS
First of all you may need a VPS out of the wall
There are way too many choises here:
[budgetvm](https://www.budgetvm.com/)		$25/year
[bandwagonhost](http://www.laozuo.org/go/bandwagonhost-64m)	$3.99/year 
other Links:
[YardVPS,Virpus,BuyVM,BudgetVM](http://www.freehao123.com/yardvps-virpus/)
[bandwagonhost from laozuo](http://www.laozuo.org/3269.html)

More prise more stable, it's your choise

## Server
There are varies way to install shadowsocks with NPM,python or you can install with source.
While I installed my server with NPM.
If you have any problem, try another way for luck.  

### NPM
#### Install Node
##### Debian and Ubuntu
``` bash
apt-get install curl
curl -sL https://deb.nodesource.com/setup | sudo bash -
sudo apt-get install -y nodejs
```
##### RHEL, CentOS or Fedora
``` bash
curl -sL https://rpm.nodesource.com/setup | bash -
#or you can
#yum install epel-release
yum install -y nodejs
```
##### 源码安装
如果以上都不行的话，就源码安装吧。
``` bash
yum -y install gcc make gcc-c++ openssl-devel wget
wget http://nodejs.org/dist/v0.10.26/node-v0.10.26.tar.gz
tar -zvxf node-v0.10.26.tar.gz
cd node-v0.10.26
make
make install
node -v
```
#### Install shadowsocks
``` bash
npm install -g shadowsocks
```
#### Config shadowsocks
在任一目录，比如新建个/root/shadowsocks目录下创建文件config.json,这个就是ss的配置文件了。
``` bash
{
    "server":"198.98.117.102", //这里是你vps的ip地址
    "server_port":8388, //服务器端监听端口
    "local_port":1080, //客户端监听端口，这里可无视
    "password":"barfoo!", //连接密码，随便射一个
    "timeout":600, //超时时间，默认即可
    "method":"aes-256-cfb" //加密方式，建议用“aes-256-cfb”，当然你也可以选择table。。。
}
```
比如我的配置，大家也可以使用，就是bandwagonhost的，有时候要经常重启
``` bash
{
    "server":"104.224.161.153",
    "server_port":8388,
    "local_port":1080,
    "password":"edmund",
    "timeout":600,
    "method":"aes-256-cfb"
}
```
开机自启动
编辑vps的rc.local，加入
``` bash
nohup ssserver -c /root/shadowsocks/config.json > log &
```
---
### Python
easy way to use, [Offical Site](https://github.com/shadowsocks/shadowsocks) also list the way to [install](https://github.com/shadowsocks/shadowsocks/wiki/Shadowsocks-%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E) and [windows version](https://github.com/shadowsocks/shadowsocks/wiki/Install-Shadowsocks-Server-on-Windows)

---
### Source
``` bash
yum install git build-essential autoconf libtool openssl-devel gcc -y
git clone https://github.com/madeye/shadowsocks-libev.git
cd shadowsocks-libev
./configure 
make && make install
```
启动
``` bash
nohup /usr/local/bin/ss-server -s IP地址 -p 端口 -k 密码 -m 加密方式 &
```
示例
nohup /usr/local/bin/ss-server -s 11.22.33.44 -p 12345 -k 12345678 -m aes-256-cfb &
其中
-s 11.22.33.44 #指定服务器的IP地址，建议填0.0.0.0
-p 12345 #指定服务器绑定的IP地址
-k 12345678 #设置密码
-m aes-256-cfb #指定加密方式为aes-256-cfb，如果不指定，默认为table方式，加密方式不大会影响速度，但是table非常不安全。
加入开机启动：
``` bash
echo "nohup /usr/local/bin/ss-server -s 11.22.33.44 -p 12345 -k 12345678 -m aes-256-cfb &" >> /etc/rc.local
```
请把IP 端口 密码 加密方式改成自己设置的。
检测shadowsocks是否在运行：
``` bash
ps -ef | grep ss-server | grep -v ps | grep -v grep
```
当然要开防火墙
``` bash
iptables -F
iptables -A INPUT -p tcp --dport 端口 -j ACCEPT
```
---
## Client
[various client](https://shadowsocks.com/client.html),
MAC推荐GoagentX，支持各种协议、PAC，直接新建一个shadowsocks代理，里面全部按照服务器的配置就好。可以全局或者规则使用了。
Windows推荐Goagent+，也是同样的配置一个shadowsocks，但是每个程序要自己去连代理，比如chrome的话要装switchysharp去连本地端口。


参考：
[Centos搭建Shadowsocks的教程，并用Chrome成功访问Google](http://www.v5fm.com/centos-shadowsocks.html)
[ShadowSocks从入门到私通](http://dou.lu/1040.x)
[Installing Node.js via package manager](https://github.com/joyent/node/wiki/installing-node.js-via-package-manager)
[VPS + Shadowsocks + COW + Ocserv + AnyConnect = 多平台翻墙解决方案](http://deffi.info/2014/11/20/VPS-+-Shadowsocks-+-COW-+Ocserv-+-AnyConnect-=-%E5%A4%9A%E5%B9%B3%E5%8F%B0%E7%BF%BB%E5%A2%99%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88/)
[If U dont wanna deploy](http://firedfox.tk/shadowsocks/)

