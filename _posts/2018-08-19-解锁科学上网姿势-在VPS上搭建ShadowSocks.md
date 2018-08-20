---
layout:     post
title:      解锁科学上网姿势-在VPS上搭建ShadowSocks
subtitle:   十分钟内让你科学上网
date:       2018-08-19  
author:     zeroGoZhang
header-img: img/post-bg-ioses.jpg
catalog: true
tags:
    - Blog
    - ShadowSocks
---

> 夫千里之行，始于足下。苟自强不息，亦何远而不届哉？
>
> [我的的博客](https://github.com/zeroGozhang/zeroGoZhang.github.io)

# 前言
年少时不懂如何科学上网，买了一些第三方的VPN，发现比较贵而且问题也多。后来决定自己搭建一个SS，网上教程也比较多，但也是有一些坑，这里记录了一下我已经成功的方法。

# 购买国外VPS（虚拟机）
1、 登录[搬瓦工](https://bwh1.net/index.php)的VPS,已经有国外VPS的可以跳过这一步

2、自己用的VPS可以不用买配置太高的的，土豪随意
![](https://ws2.sinaimg.cn/large/006tNbRwgy1fufa29bv9oj31kw0trkfd.jpg)

# 配置SS

1、点击进入Order KVM or OpenVZ
   购买 KVM 或者 OVZ
   >KVM跟OVZ 这两者的区别是可以[这里](https://banwagong.cn/ovz-kvm.html) https://banwagong.cn/ovz-kvm.html 查看，有兴趣的朋友可以点击进入看一下

2、
 在Services - My Services 里面找到你刚刚购买的机器，点击Control Panel
![](https://ws3.sinaimg.cn/large/006tNbRwgy1fufalfx6mdj31kw0tt0zq.jpg)

3、进入控制台 -> Root Shell-Interactive，输入你的用户名跟密码（购买完会发邮件到你的邮箱）
输入
```shell
wget http://w.huizhanzhang.com/shadowsocks.sh && chmod +x shadowsocks.sh &&./shadowsocks.sh 2>&1 | tee shadowsocks.log
```
4、
> vi /etc/shadowsocks/config.json

可以看到一串json文件模板
```
{
    "server":"0.0.0.0",
    "local_port":1080,
    "port_password":{
        "port1": "port_password1",
        "port2": "port_password2"
    },
    "method":"aes-256-cfb",
    "timeout":600
}
```

修改port为你想要访问的port， port_password用于你访问的密码

5、修改完毕，输入/etc/init.d/shadowsocks restart

6、Windows, Mac, IOS, Android各个端使用SS方案 可以戳[这里](https://crifan.github.io/scientific_network_summary/website/server_client_mode/ss_client/client_ios.html)

# 结语

最后祝大家都可以上科学上网，走向地球村
