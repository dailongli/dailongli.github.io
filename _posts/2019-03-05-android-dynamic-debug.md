---
layout: post
title: Androi动态调试
---


1.解压apk
```
apktool decode NewGloryPlaza.apk
```
2.修改AndroidManifest.xml
```
<application android:debuggable="true" 
</application>
```
3.重新打包到NewGloryPlaza\dist\NewGloryPlaza.apk
```
apktool build NewGloryPlaza
```
4.生成签名文件qj.keystore 
```
keytool -genkeypair -alias qj.keystore -keyalg RSA -validity 36000 -keystore qj.keystore 
```
5.签名
```
jarsigner -verbose -keystore qj.keystore -signedjar signed.apk NewGloryPlaza\dist\NewGloryPlaza.apk qj.keystore
```
6.安装apk
```
adb install signed.apk
```




0.上传android_sever并修改权限
```
adb push "C:\Program Files (x86)\IDA 6.8\dbgsrv\android_server" /data/local/tmp/
adb shell chmod 755 /data/local/tmp/android_server
```
1.以root权限执行android_server
```
adb shell
su
/data/local/tmp/android_server
```
2.端口映射
```
adb forward tcp:23946 tcp:23946
```
3.调试模式启动
```
adb shell am start -D -n foxuc.qp.Gloqj/org.cocos2dx.lua.AppActivity
```
4.Attach进程


5
```
adb jdwp
adb forward tcp:8700 jdwp:22183
```

6
```
jdb -connect com.sun.jdi.SocketAttach:hostname=127.0.0.1,port=8700
```



