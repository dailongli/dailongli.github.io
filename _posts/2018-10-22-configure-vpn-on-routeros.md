---
type: post
title: RouterOS配置VPN服务
---


1. 下载WinBox登录RouterOS

2. 创建l2tp-pool地址池
IP ---> Pool ---> New IP Pool
Name:      l2tp-pool
Addresses: 10.10.10.2-10.10.10.254
Next Pool: none

3. 创建l2tp-profile
PPP ---> Profiles ---> New PPP Profile
Name:           l2tp-profile
Local Address:  10.10.10.1
Remote Address: lt2p-pool
DNS Server:     1.1.1.1

4. 开启L2TP服务器
PPP ---> Interface ---> L2TP Server
Default Profile: l2tp-profile

5. 创建l2tp接口
PPP ---> Interface ---> Add ---> L2tp Server
Name: l2tp-in1
Type: L2TP Server

6. 创建PPP用户密码
PPP ---> Secrets ---> Add ---> New PPP Secret
Name:     username
Password: password
Service:  l2tp
Profile:  l2tp-profile

 
