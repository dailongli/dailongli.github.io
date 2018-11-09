---
layout: post
title: Android NDK
---

jni/Android.mk

```
# my-dir宏函数返回Android.mk所在目录，即jni/目录
LOCAL_PATH := $(call my-dir)
```

```
# 清除LOCAL_MODULE, LOCAL_SRC_FILES, LOCAL_STATIC_LIBRARIES等变量
include $(CLEAR_VARS)
# 你要编译的模块名为libhello-jni.so
LOCAL_MODULE := hello-jni
# 指定源文件
LOCAL_SRC_FILES := hello-jni.c
# 编译为共享库
include $(BUILD_SHARED_LIBRARY)
```
