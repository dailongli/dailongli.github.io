---
layout: post
title: Lua编程
---

Lua一共包含8个基本数据类型
```
nil:        print(type(nil))
boolean:    print(type(true))
number:     print(type(2.0))
string:     print(type("abc"))
function:   print(type(type))
userdata:
thread:     print(type(coroutine.create(function()end)))
table:      print(type({}))
```


Lua标准库包括以下10个库:
```
基本库
pcall (f [, arg1, ···])
xpcall (f, msgh [, arg1, ···])
```

```
协程操作库
coroutine.create(function(i) print(i); end)
coroutine.isyieldable ()
coroutine.resume (co [, val1, ···])
coroutine.running ()
coroutine.status (co)
coroutine.wrap (f)
coroutine.yield (···)
```

```
包库
require()
package.config
package.cpath
package.loaded
package.loadlib (libname, funcname)
package.path
package.preload
package.searchers
package.searchpath (name, path [, sep [, rep]])
```

字符串操作
基本UTF-8支持
表操作库
数学计算库
输入输出库
操作系统工具库

```
调试库
debug.debug ()
debug.gethook ([thread])
debug.getinfo ([thread,] f [, what])
debug.getlocal ([thread,] f, local)
debug.getmetatable (value)
debug.getregistry ()
debug.getupvalue (f, up)
debug.getuservalue (u)
debug.sethook ([thread,] hook, mask [, count])
debug.setlocal ([thread,] level, local, value)
debug.setmetatable (value, table)
debug.setupvalue (f, up, value)
debug.setuservalue (udata, value)
debug.traceback ([thread,] [message [, level]])
debug.upvalueid (f, n)
debug.upvaluejoin (f1, n1, f2, n2)
```

