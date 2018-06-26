
---
layout: post
title: "Nginx源码安装与配置"
---


// 安装build-essential
// http_rewrite_module模块需要PCRE库
// http_gzip_module模块需要zlib库
// libssl-dev可选,如果需要支持https
```
sudo apt-get -y install build-essential libpcre3-dev zlib1g-dev libssl-dev
```


// 下载编译和安装
打开https://nginx.org/en/download.html，下载最新版本
```
wget http://nginx.org/download/nginx-1.14.0.tar.gz
tar -xvzf nginx-1.14.0.tar.gz
cd nginx-1.14.0/
./configure --with-http_ssl_module --with-http_v2_module
make
sudo make install
```

// 创建开机自动启动脚本文件
```
sudo touch /lib/systemd/system/nginx.service
```

```
# Stop dance for nginx
# =======================
#
# ExecStop sends SIGSTOP (graceful stop) to the nginx process.
# If, after 5s (--retry QUIT/5) nginx is still running, systemd takes control
# and sends SIGTERM (fast shutdown) to the main process.
# After another 5s (TimeoutStopSec=5), and if nginx is alive, systemd sends
# SIGKILL to all the remaining processes in the process group (KillMode=mixed).
#
# nginx signals reference doc:
# http://nginx.org/en/docs/control.html
#
[Unit]
Description=A high performance web server and a reverse proxy server
After=network.target

[Service]
Type=forking
PIDFile=/usr/local/nginx/logs/nginx.pid
ExecStartPre=/usr/local/nginx/sbin/nginx -t -q -g 'daemon on; master_process on;'
ExecStart=/usr/local/nginx/sbin/nginx -g 'daemon on; master_process on;'
ExecReload=/usr/local/nginx/sbin/nginx -g 'daemon on; master_process on;' -s reload
ExecStop=-/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /usr/local/nginx/logs/nginx.pid
TimeoutStopSec=5
KillMode=mixed

[Install]
WantedBy=multi-user.target
```


```
// 启动nginx
systemctl start nginx.service

// 停止nginx
systemctl stop nginx.service

// 查看nginx运行状态
systemctl status nginx.service


// 开机启动
systemctl enable nginx.service

// 开机不启动
systemctl disable nginx.service
```


```
touch /etc/logrotate.d/nginx
```

```
/usr/local/nginx/logs/access.log {
        daily
        missingok
        rotate 12
        compress
        notifempty
}

/usr/local/nginx/logs/error.log {
        daily
        missingok
        rotate 12
        compress
        notifempty
}
```
