---
layout: post
title: "metasploit"
---

```
apt install -y build-essential zlib1g zlib1g-dev libpq-dev libpcap-dev libsqlite3-dev ruby ruby-dev
```

```
git clone https://github.com/rapid7/metasploit-framework.git
cd metasploit-framework/
sudo gem install bundler
bundle install

ln -s /root/metasploit-framework/msfconsole /usr/local/bin/


git config --global user.name "NAME HERE"
git config --global user.email "email@example.com"
./msfupdate

crontab -e
0 1 * * * /root/metasploit-framework/msfupdate > /dev/null 2>&1
```
