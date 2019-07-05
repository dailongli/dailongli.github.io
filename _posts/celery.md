---
layout: post
title: Python Celery
---


```
$ celery -A app.tasks worker -l info

$ redis-cli
127.0.0.1:6379> keys *
1) "_kombu.binding.celery.pidbox"
2) "_kombu.binding.celeryev"
3) "unacked_mutex"
4) "_kombu.binding.celery"


```
