---
layout:     post
title:      "Java Servlet URL重定向路径符号问题"
subtitle:   " \"Hello World, Hello Blog, My Friend\""
date:       2018-06-27 13:26:00
author:     "南迦闲游"
header-img: "img/post-bg-Java-Servlet-Introduction-Overview-and-Life-Cycle.png"
catalog: true
tags:
    - JAVA
---

> “Yeah It's on. ”



最近在学习JAVA web Servlet 的相关知识, 有一次在测试的时候, 想从一个Servlet 通过URL重定向跳转到另外一个的时候，
本地部署总是报 "404"错误...


## 正文
检查以后发现，问题就出现在跳转路径的写法上.
```Java
resp.sendRedirect("student/list");
```

我的当前Servlet的上下文路径为:"/student/delete"
部署后,在地址栏路径为："http://localhost:8080/student/student/list"

在网上搜索了一下，问题是由于如果在路径上不是以'/'开头的,则容器将其解释为相对于当前请求的根路径加上我写的跳转路径,也就是说：
容器会去请求/student/student/list,自然就报错404.

这是我在查询后的理解，望指正!

另附：java中对于此路径参数的解释：

>"Sends a temporary redirect response to the client using the specified redirect location URL. This method can accept relative URLs;"
>"the servlet container must convert the relative URL to an absolute URL before sending the response to the client. "
>"If the location is relative without a leading '/' the container interprets it as relative to the current request URI. "
>"If the location is relative with a leading '/' the container interprets it as relative to the servlet container root. "
>"If the response has already been committed, this method throws an IllegalStateException. 
>"After using this method, the response should be considered to be committed and should not be written to."


