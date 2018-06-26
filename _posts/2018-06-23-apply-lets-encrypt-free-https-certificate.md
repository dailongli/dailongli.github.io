---
layout: post
title: "申请Let's Encrypt免费https证书"
---

Let's Encrypt提供免费https证书服务，有效期3个月过后可以renew

下载工具
```
git clone https://github.com/certbot/certbot.git
cd certbot
```



DNS方式生成证书
注意第一个域名是证书的Subject
```
./certbot-auto certonly -d "*.freetv8.com,freetv8.com,*.freetv8.xyz,freetv8.xyz" --manual --preferred-challenges dns-01  --server https://acme-v02.api.letsencrypt.org/directory
```

验证证书
```
sudo tree /etc/letsencrypt/live/freetv8.com
sudo openssl x509 -in /etc/letsencrypt/live/freetv8.com/cert.pem -noout -text
```

nginx配置
freetv8.com包括freetv8.com和www.freetv8.com
non-www转www
non-https转https
```
    server {
        listen      443 ssl http2;
        server_name .freetv8.com .freetv8.xyz;
        ssl_certificate /etc/letsencrypt/live/freetv8.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/freetv8.com/privkey.pem;
        if ($host !~ ^www\.) {
            return 301 https://www.$host$request_uri;
        }
        if ($scheme != "https") {
            return 301 https://$host$request_uri;
        } 
        location / {
            proxy_pass http://localhost:6000;
            proxy_set_header Host              $host;
            proxy_set_header X-Forwarded-For   $remote_addr;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }
```

监控证书过期
https://letsmonitor.org/

如果3个月过期需要renew
```
./certbot-auto renew
```


删除证书
```
./certbot-auto delete

```
