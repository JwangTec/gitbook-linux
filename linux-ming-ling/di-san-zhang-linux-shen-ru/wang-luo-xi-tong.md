# 3. 网络系统

1. 说明:

   当谈及到网络系统层面，几乎任何东西都能由 Linux 来实现。Linux 被用来创建各式各样的网络系统和装置， 包括防火墙，路由器，名称服务器，网络连接式存储设备等等

2. ping - 发送 ICMP ECHO\_REQUEST 软件包到网络主机 最基本的网络命令是 ping。这个 ping 命令发送一个特殊的网络数据包，叫做 IMCP ECHO\_REQUEST，到 一台指定的主机。大多数接收这个包的网络设备将会回复它，来允许网络连接验证。

   > 注意：大多数网络设备（包括 Linux 主机）都可以被配置为忽略这些数据包。通常，这样做是出于网络安全 原因，部分地遮蔽一台主机免受一个潜在攻击者地侵袭。配置防火墙来阻塞 IMCP 流量也很普遍

   ```text
    rimideiMac-10:test admin$ ping www.baidu.com
    PING www.a.shifen.com (180.97.33.108): 56 data bytes
    64 bytes from 180.97.33.108: icmp_seq=0 ttl=54 time=37.258 ms
    64 bytes from 180.97.33.108: icmp_seq=1 ttl=54 time=37.536 ms
    64 bytes from 180.97.33.108: icmp_seq=2 ttl=54 time=37.661 ms
   ```

   > 一旦启动，ping 命令会持续在特定的时间间隔内（默认是一秒）发送数据包，直到它被中断\(按下组合键 Ctrl-c\)

3. traceroute - 打印到一台网络主机的路由数据包

   这个 traceroute 程序（一些系统使用相似的 tracepath 程序来代替）会显示从本地到指定主机 要经过的所有“跳数”的网络流量列表

   ```text
    rimideiMac-10:test admin$ traceroute www.baidu.com
    traceroute: Warning: www.baidu.com has multiple addresses; using 180.97.33.108
    traceroute to www.a.shifen.com (180.97.33.108), 64 hops max, 52 byte packets
     1  * * *
     2  10.4.0.2 (10.4.0.2)  2.873 ms  1.298 ms  4.211 ms
     3  1.163.70.125.broad.cd.sc.dynamic.163data.com.cn (125.70.163.1)  24.743 ms  3.445 ms
        100.64.0.1 (100.64.0.1)  2.700 ms
     4  220.167.87.201 (220.167.87.201)  44.881 ms  7.184 ms  3.658 ms
     5  171.208.199.181 (171.208.199.181)  3.891 ms
        171.208.199.237 (171.208.199.237)  6.653 ms
        171.208.199.205 (171.208.199.205)  3.264 ms
     6  202.97.66.194 (202.97.66.194)  36.510 ms
        202.97.122.213 (202.97.122.213)  39.014 ms
        202.97.29.253 (202.97.29.253)  31.803 ms
     7  202.102.73.150 (202.102.73.150)  42.186 ms
        202.102.69.250 (202.102.69.250)  34.208 ms
        202.102.73.150 (202.102.73.150)  38.738 ms
   ```

   > 对于那些没有提供标识信息的路由器（由于路由器配置，网络拥塞，防火墙等 方面的原因），我们会看到几个星号

4. netstat - 打印网络连接，路由表，接口统计数据，伪装连接，和多路广播成员

   程序被用来检查各种各样的网络设置和统计数据。通过此命令的许多选项，我们 可以看看网络设置中的各种特性。使用“-ie”选项\(或者ifconfig\)，我们能够查看系统中的网络接口：

   ```text
    rimideiMac-10:test admin$ ifconfig 
   lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST> mtu 16384
    options=1203<RXCSUM,TXCSUM,TXSTATUS,SW_TIMESTAMP>
    inet 127.0.0.1 netmask 0xff000000 
    inet6 ::1 prefixlen 128 
    inet6 fe80::1%lo0 prefixlen 64 scopeid 0x1 
    nd6 options=201<PERFORMNUD,DAD>
   gif0: flags=8010<POINTOPOINT,MULTICAST> mtu 1280
   stf0: flags=0<> mtu 1280
   XHC20: flags=0<> mtu 0
   en0: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
    options=10b<RXCSUM,TXCSUM,VLAN_HWTAGGING,AV>
    ether ac:87:a3:2a:ef:b5 
    nd6 options=201<PERFORMNUD,DAD>
    media: autoselect (none)
    status: inactive
   en1: flags=8863<UP,BROADCAST,SMART,RUNNING,SIMPLEX,MULTICAST> mtu 1500
    ether b8:09:8a:c7:ac:e5 
    inet6 fe80::8a1:d9f6:338c:5833%en1 prefixlen 64 secured scopeid 0x6 
    inet 10.2.1.64 netmask 0xfffff800 broadcast 10.2.7.255
    nd6 options=201<PERFORMNUD,DAD>
    media: autoselect
    status: active
   ```

   > 第一个，叫做 eth0，是 因特网接口，和第二个，叫做 lo，是内部回环网络接口，它是一个虚拟接口，系统用它来 “自言自语” eth1 内网地址

5. wget - 非交互式网络下载器

```text
    wget www.baidu.com
```

