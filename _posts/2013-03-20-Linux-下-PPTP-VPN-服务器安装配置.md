---
layout: post
category: 服务器
tags: Linux vpn
description: 在 Debian 上搭建基于 PPTP 的 VPN 服务器。可以在 Linux 或 Windows 上登陆上网。如果服务器是国外的还可以直接翻墙，这比什么其它代理强多了
---

### 服务器安装配置

  1. 安装 PPTP

        aptitude install pptpd

  2. 配置 PPTP
    * 修改 `/etc/pptpd.conf`

            localip 200.110.30.4        # localip 为你服务器的 ip
            remoteip 192.168.100.234-238,192.168.100.245      # remoteip 为服务器分配给登陆 VPN 客户端的 ip 范围
    * 修改 `/etc/ppp/pptpd-options`，修改为你自己的 DNS 服务器 或者就用本文中 Google DNS 服务器
  
            ms-dns 8.8.8.8
            ms-dns 4.4.4.4
    * 修改 `/etc/ppp/chap-secrets`， 添加用户名和密码

            <username>      pptpd   <password>        *
    * 修改 `/etc/sysctl.conf`，才可以上网

            # Uncomment the next line to enable packet forwarding for IPv4
            net.ipv4.ip_forward=1

  3. 配置防火墙

        iptables -t nat -A POSTROUTING -s 192.168.100.0/24 -o eth0 -j MASQUERADE


  4. 重启服务器，`reboot` 后就可以在客户端进行连接了

### 客户端安装配置

  由于客户端多种多样，因此我就不一一列举了，只是大体说明下

  1. Linux 客户端可以通过 pptp 命令链接，也可以使用 network-manager 连接
  2. Windows 客户端可以打开网络共享中心 设置新的链接或网络 选择 连接到工作区 
