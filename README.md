# unbound.conf

![unbound.conf](https://i.imgur.com/zoFgNsM.png)

[DNSCrypt](https://dnscrypt.org/) is a piece of lightweight software that everyone should use to boost online privacy and security. It works by encrypting all DNS traffic between the user and DNS resolver, preventing any spying, spoofing or man-in-the-middle attacks.

[Unbound](https://www.unbound.net/) is a validating, recursive, and caching DNS resolver. 

[NirCmd](http://www.nirsoft.net/utils/nircmd.html) is a small command-line utility that allows you to do some useful tasks without displaying any user interface.

## 使用方法

* 下载 [DNSCrypt](https://download.dnscrypt.org/dnscrypt-proxy/dnscrypt-proxy-win32-full-1.6.1.zip)、[Unbound](http://unbound.net/downloads/unbound-1.5.8.zip)、[NirCmd 32-bit](http://www.nirsoft.net/utils/nircmd.zip)或[NirCmd 64-bit](http://www.nirsoft.net/utils/nircmd-x64.zip)

* 解压`dnscrypt-proxy-win32-full-1.6.1.zip`到`E:\Program Files\DNSCrypt\`；解压`unbound-1.5.7.zip`到`E:\Program Files\unbound\`；解压`nircmd.zip`或`nircmd-x64.zip`到`C:\Windows\System32\`

* 下载[配置文件](https://github.com/CNMan/unbound.conf/archive/master.zip)并解压到`E:\Program Files\unbound\`

* 根据实际情况修改[localdns.cmd](https://github.com/CNMan/unbound.conf/blob/master/localdns.cmd)和[配置文件](https://github.com/CNMan/unbound.conf/blob/master/unbound.conf)中的相关目录

* 运行localdns.cmd启动DNSCrypt和Unbound

* 在网络设置里面把DNS服务器设置成127.0.0.1

* 将localdns.cmd放到`C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp\`目录，开机自动启动

![localdns](https://i.imgur.com/4WN9qit.png)

## 说明

常用hosts域名配置在unbound.local-zone.hosts.conf；广告域名和恶意软件域名配置在unbound.local-zone.block.conf。配置说明可参考[Unbound+DNSCrypt双保险防DNS污染及劫持](https://goo.gl/IG3K27)

国内域名默认由114.114.114.114和223.5.5.5解析，配置在[unbound.forward-zone.China.conf](https://github.com/CNMan/unbound.conf/blob/master/unbound.forward-zone.China.conf)；其他域名默认由监听在9999端口的DNSCrypt解析

修改unbound配置文件后，请先检查有没有错误配置，再重启unbound并刷新DNS解析缓存

```
cd /d "E:\Program Files\unbound\"
unbound-checkconf unbound.conf
unbound-control -c unbound.conf reload
ipconfig /flushdns
```

![unbound-control](https://i.imgur.com/FWjHwjh.png)

## 致谢

* hosts域名列表取自[https://github.com/racaljk/hosts](https://github.com/racaljk/hosts)

* 广告域名列表取自[http://pgl.yoyo.org/adservers/serverlist.php?showintro=0](http://pgl.yoyo.org/adservers/serverlist.php?showintro=0)

* 恶意软件域名列表取自[http://www.malware-domains.com/files/immortal_domains.zip](http://www.malware-domains.com/files/immortal_domains.zip)

* 国内域名列表取自[dnsmasq-china-list](https://github.com/felixonmars/dnsmasq-china-list)，如果你有其他国内域名需要添加，请直接向`dnsmasq-china-list`项目反馈
