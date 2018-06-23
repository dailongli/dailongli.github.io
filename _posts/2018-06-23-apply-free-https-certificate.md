---
layout: post
title: "免费https证书申请与配置"
---


git clone https://github.com/certbot/certbot.git
cd certbot
./certbot-auto certonly  -d "*.freetv8.com" -d "freetv8.com" --manual --preferred-challenges dns-01  --server https://acme-v02.api.letsencrypt.org/directory

sudo tree /etc/letsencrypt/live/freetv8.com
sudo openssl x509 -in /etc/letsencrypt/live/freetv8.com/cert.pem -noout -text


    server {
        listen      443 ssl http2;
        server_name *.freetv8.com;
        ssl_certificate /etc/letsencrypt/live/freetv8.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/freetv8.com/privkey.pem;
        location / {
            proxy_pass http://localhost:6000;
            proxy_set_header Host              $host;
            proxy_set_header X-Forwarded-For   $remote_addr;
            proxy_set_header X-Forwarded-Proto $scheme;
        }
    }


https://letsmonitor.org/


./certbot-auto renew
