---
layout: post
title: "Ubuntu下配置IKEv2 VPN"
---


```
sudo apt install strongswan
sudo vim /etc/ipsec.conf
```

```
config setup

conn ikev2-vpn
    auto=add
    compress=no
    type=tunnel
    keyexchange=ikev2
    fragmentation=yes
    forceencaps=yes
    ike=aes256-sha1-modp1024,3des-sha1-modp1024!,aes256-sha2_256
    esp=aes256-sha1,3des-sha1!
    dpdaction=clear
    dpddelay=300s
    rekey=no
    left=%any
    leftid=%any
    leftsubnet=0.0.0.0/0
    right=%any
    rightid=%any
    rightdns=8.8.8.8,8.8.4.4
    rightsourceip=10.10.10.0/24
    authby=secret
```

```
sudo vim /etc/ipsec.secrets
: PSK thisispresharedkey

sudo service strongswan restart
```

```
sudo sysctl -w net.ipv4.ip_forward=1



sudo vim /etc/sysctl.conf
net.ipv4.ip_forward=1
```


```
ifconfig find interface
sudo iptables -t nat -A POSTROUTING -s 10.10.10.10/24 -o eth0 -j MASQUERADE

sudo iptables -L -t nat


sudo apt-get install iptables-persistent
sudo netfilter-persistent save
sudo netfilter-persistent reload
```




