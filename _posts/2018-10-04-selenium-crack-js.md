---
layout: post
title: "使用Selenium破解js"
---

<a href="https://www.seleniumhq.org/" target="_blank">Selenium</a>是一个基于浏览器的自动化测试工具。中文意思是硒。



```
pip install -U selenium
```


下载最新的<a href="https://sites.google.com/a/chromium.org/chromedriver/downloads" target="_blank">ChromeDriver</a>并保存为/usr/local/bin/chromedriver
```
$chromedriver -h
Usage: chromedriver [OPTIONS]

Options
  --port=PORT                     port to listen on
  --adb-port=PORT                 adb server port
  --log-path=FILE                 write server log to file instead of stderr, increases log level to INFO
  --log-level=LEVEL               set log level: ALL, DEBUG, INFO, WARNING, SEVERE, OFF
  --verbose                       log verbosely (equivalent to --log-level=ALL)
  --silent                        log nothing (equivalent to --log-level=OFF)
  --version                       print the version number and exit
  --url-base                      base URL path prefix for commands, e.g. wd/url
  --port-server                   address of server to contact for reserving a port
  --whitelisted-ips               comma-separated whitelist of remote IPv4 addresses which are allowed to connect to ChromeDriver
```

运行chromedriver，默认监听9515端口
```
$chromedriver
Starting ChromeDriver 2.38.552518 (183d19265345f54ce39cbb94cf81ba5f15905011) on port 9515
Only local connections are allowed.
```
