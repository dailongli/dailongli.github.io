---
layout: post
title: "MacOS下跨平台编译android libiconv库"
---

libiconv是一个字符编码转换库, Android NDK

```
$ wget https://ftp.gnu.org/pub/gnu/libiconv/libiconv-1.15.tar.gz
$ tar -xvzf libiconv-1.15.tar.gz
$ cd libiconv-1.15
$ ./configure
$ mkdir jni
$ touch jni/Android.mk
```

```
LOCAL_PATH := $(call my-dir)

include $(CLEAR_VARS)
TARGET_ARCH_ABI := armeabi-v7a
LOCAL_MODULE	:= iconv
LOCAL_CFLAGS	:= \
	-Wno-multichar \
	-D_ANDROID \
	-DLIBDIR="\"c\"" \
	-DBUILDING_LIBICONV \
	-DIN_LIBRARY
LOCAL_C_INCLUDES	:= \
	../libiconv-1.15 \
	../libiconv-1.15/include \
	../libiconv-1.15/lib \
	../libiconv-1.15/libcharset/include \
LOCAL_SRC_FILES	:=\
	../libiconv-1.15/lib/iconv.c \
	../libiconv-1.15/lib/relocatable.c \
	../libiconv-1.15/libcharset/lib/localcharset.c \

include $(BUILD_SHARED_LIBRARY)
```

```
$ ndk-build V=1
$ ls -l ../libs
```
