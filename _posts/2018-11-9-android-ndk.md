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
# 添加include路径
LOCAL_C_INCLUDES := $(LOCAL_PATH)/../../Classes/foo
# 包含依赖的库，链接器会去除掉库文件中没有使用的死代码
LOCAL_STATIC_LIBRARIES := cocos2d_lua_static
LOCAL_STATIC_LIBRARIES += other_static
# 类似LOCAL_STATIC_LIBRARIES，但包含静态库的所有源代码
LOCAL_WHOLE_STATIC_LIBRARIES += mc_kernel_static
# 共享库
include $(BUILD_SHARED_LIBRARY)
# 预编译共享库(LOCAL_SRC_FILES指向库文件路径)
include $(PREBUILT_SHARED_LIBRARY)
```

```
# 自动加载其他Android.mk文件
$(call import-module, external/bugly)
```
