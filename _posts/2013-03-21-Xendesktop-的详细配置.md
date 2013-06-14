---
layout: post
category: 服务器
tags: Xendesktop Windows
description: 详细介绍 Xendesktop Studio 配置使用，如何用 Xendesktop 来搭建虚拟桌面。 以及搭建 Xendesktop 最常见的问题 “未注册” 的解决办法
---

### 配置 Licence Server
  1. 如果你已经有许可证服务器或者还没有购买许可者，则此步可以省略。

  2. 配置步骤：

        在 安装 Xendesktop 的计算机上
        打开 "开始菜单" -> "所有程序" -> "Citrix" -> "管理控制台"  -> "许可证管理控制台" -> 
        点击右上角 "管理"  -> 
        用域管理员（用户名：ad\admin）登录  -> 
        选择 "供应商守护程序配置" -> 
        选择 "导入许可证"，浏览本地许可证位置，点击 "导入许可证" -> 
        单击 "确定"，导入成功
        然后依次重启 "Citrix Licensing"，"Citrix Licensing Config Service"，"Citrix Licensing 支持服务"
        当我们再次打开 许可证控制台 就可以看到所有可用的许可证了

### Desktop Studio初始配置

    在 安装 Xendesktop 的计算机上
    打开 "开始菜单" -> "所有程序" -> "Citrix" -> "Desktop Studio" -> 
    选择 "桌面部署" -> 
    输入站点名称 "TestXenDesktop"，数据库配置选择 "使用默认数据库"，然后 "下一步" -> 
    提示找不到数据库，是否为你在服务器上创建数据库，选择 "确定" -> 
    在 许可证服务器中填入你的许可证服务器地址，默认 localhost:27000，然后选择许可证版本，然后 "下一步" -> 
    主机类型选择 "Citrix XenServer"，地址为 Xenserver 服务器地址，用户名，密码也为 Xenserver 服务器用户名和密码。输入连接名称 "XenServer One"，选择 "使用 Xendesktop 创建虚拟机"，然后 "下一步" -> 
    设置主机名和网卡（网卡为 Xenserver 上的网卡），然后 "下一步" -> 
    选择存储 "为虚拟机和 Personal vDisk 使用相同的存储"，然后 "下一步" -> 
    单击 "完成"。OK 了
  

### 批量发布虚拟桌面
  1. 配置此步之前，确定已经制作好了模板镜像

  2. 虚拟桌面配置

        打开 "Desktop Studio" -> 点击 计算机创建中的 "配置" 按钮-> 
        在计算机类型中选择 "池"，计算机分配中选择 "随机 - 在用户登录时为用户随机分配计算机"，然后 "下一步" -> 
        选择主映像为模板镜像，然后 "下一步" -> 
        设置要创建虚拟机数，Active Directory 计算机账户选择 "创建新账户"，然后 "下一步" -> 
        选择计算机账户的 Active Directory 位置为 "computers"，设置账户命名方案（其中 `#` 为占位符，可表示 0-9 或者 a-z ），然后 "下一步" ->  "下一步" -> 
        设置目录名称 "Test Windows 7"，然后 "完成"

  3. 创建用户组

        打开 "Desktop Studio" -> 右键单击 "分配"  -> 选择 "创建桌面组" ->
        选择刚创建的目录 "Test Windows 7" 下面出现添加计算机，输入要分配的计算机台数，然后 "下一步" -> 
        选择可以使用这些计算机的用户和组，然后 "下一步" -> "下一步" -> 
        最后设置显示名称（用户可见），桌面组名称（方便服务器辨别），然后 "完成"

  4. 未注册解决   
    注意：Desktop Studio 会自动对桌面组进行电源管理。如果在虚拟机启动后出现 "未注册"，则按如下步骤检测：

        确定虚拟机的和 Xendesktop Studio 位于同一域中
        确定虚拟机可以 ping 通 Xendesktop Studio 的 主机名.ad.test.com
        确定虚拟机的防火墙以关闭
        
  5. 测试虚拟桌面

        在其它可访问到 Xendesktop Studio 的客户机上：
        打开 IE，或者 Firefox，然后输入 Xendesktop Studio 的 IP，
        如果安装了 "Citrix Receiver"，则会出现登录界面，否则会提示安装。
        登录成功后，会点亮图标，并会自动打开客户端。如果没有打开，可点击浏览器中图标

### 配置带个人盘的虚拟桌面
  1. 带个人盘（Personal vDisk）的好处是，在用户重启计算机后可以保存用户数据。

  2. 配置说明：
    * 在安装 Xendesktop Agent 是选择 "是，启用 Personal vDisk"，其它步骤和前一篇 制作模板镜像 中的步骤一样，安装后 "更新 Personal vDisk"，更新完后关机。
    * 在 虚拟桌面配置 时，不选择 "池"，而是选择 "通过 Personal vDisk 进行池化"，其它步骤和前面批量发布虚拟桌面 2 中的一样一样。
