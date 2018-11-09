---
layout: post
title: Android NDK
---

jni/Android.mk

```
# 必须第一行，返回jni/目录
LOCAL_PATH := $(call my-dir)
```

```
# 清除LOCAL_MODULE, LOCAL_SRC_FILES, LOCAL_STATIC_LIBRARIES等变量
include $(CLEAR_VARS)
# 编译的库名为libhello-jni.so
LOCAL_MODULE := hello-jni
# 覆盖LOCAL_MODULE变量，编译的库名为libnewfoo.so
LOCAL_MODULE_FILENAME := libnewfoo
# 指定源文件
LOCAL_SRC_FILES := hello-jni.c

# 共享库
include $(BUILD_SHARED_LIBRARY)
# 预编译共享库(LOCAL_SRC_FILES指向库文件路径)
include $(PREBUILT_SHARED_LIBRARY)
```
