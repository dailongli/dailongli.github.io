---
type: post
title: 网狐荣耀版安装
---

操作系统设置

Region
Format: Chinese
Language for non-Unicode programs: Chinese

```
安装数据库(一共9个)
双击 数据库脚本/大厅脚本/一键安装
双击 数据库脚本/网站脚本/一键安装
```


```
编译系统模块(一共27个项目)
VS2003打开 系统模块/Platform 编译生产发布组件和运行文件夹
```

```
打开IP配置器/Collocate.exe生成Serverparameter.ini, 复制到运行/Release/Unicode文件夹内
```

```
VS2017打开WHRYWEB/RYAdmin/RYAdmin.sln
修改web.config数据库连接密码
Build ---> Publish
```

```
编译子游戏
打开游戏组件/官方正版/荣耀正版三通_财富_二人牛牛/GameProject.sln
检查运行/release/unicode下是否有OxExServer.DLL
```

```
登录后台
系统维护 机器管理 新增
机器名称: test
地址: 192.168.59.156
端口: 1433
帐号: sa
密码: **********

系统维护 游戏管理 模块 新增
模块标识: 102
模块名称: 二人牛牛
数据库名: RYTreasureDB
数据库地址: test
服务端版本号: 6.7.0.1
客户端版本号: 6.7.0.1
服务端名称: OxExServer.DLL
客户端名称: OxEx.exe
支持类型: 所有

 # 查看二人牛牛服务端头文件CMD_Ox.h 
 #define KIND_ID 102
模块标识102

#define VERSION_SERVER PROCESS_VERSION(7,0,1)
#define VERSION_CLIENT PROCESS_VERSION(7,0,1)
即版本6.7.0.1



系统维护 游戏管理 游戏 新增
游戏标识: 102
游戏名称: 二人牛牛
游戏类型: 棋牌游戏
挂接: 无挂接
排序: 0
模块名称: 二人牛牛
进程名字: OxEx.exe
赢一局经验: 0
游戏属性: 热
禁用状态:　正常
是否存在移动版: 打勾

系统维护 游戏管理 手游 新增
游戏标识：102
游戏名称：二人牛牛
模块名称：	yule.oxex
模块版本号：	6.7.0.1
资源版本号：8
排序：0
游戏归属：ios	android
禁用状态：	正常

//模块名称查看Phone/client/game/yule/oxex　文件夹压缩oxex.zip
放在RYFront/download/game/yule/oxex.zip

```
