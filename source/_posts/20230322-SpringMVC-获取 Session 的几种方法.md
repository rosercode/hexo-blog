---
title: Spring MVC | SpringMVC-获取 Session 的几种方法.md
date: 2023-03-22 12:00:00
tags:



---

SpringMVC-获取 Session 的几种方法.md

<!-- more --> 
## 方法1：方法的参数列表

```java
@PostMapping(value = "/msg1")
@ApiOperation("获取用户信息")
public GlobalResult msg1(HttpSession session){
    UserMsgResp userMsg = (UserMsgResp) session.getAttribute("userMsg");
    return GlobalResult.success(userMsg);
}
```

或者

```java
@PostMapping(value = "/msg1")
@ApiOperation("获取用户信息")
public GlobalResult msg1(@Autowired HttpSession session){
    UserMsgResp userMsg = (UserMsgResp) session.getAttribute("userMsg");
    return GlobalResult.success(userMsg);
}
```

## 方法2：RequestContextHolder

RequestContextHolder，顾名思义,持有上下文的Request容器.

```java
@PostMapping(value = "/msg1")
@ApiOperation("获取用户信息")
public GlobalResult msg1(){
    HttpServletRequest request = ((ServletRequestAttributes) RequestContextHolder.getRequestAttributes()).getRequest();
    HttpSession session = request.getSession();
}

```

根据你的需求，选择合适的方法来获取 HttpSession

我根据喜欢使用第二种方式来获取 HttpSession，因为相对于第一种方式，第二种方式有下面的优点

1. 更加灵活。你可以在 service 层直接获取到 HttpSession，而不需要 controller 传入。
2. 不占用参数列表。在参数列表中添加 HttpSession，swagger2 会出现相关的内容。

> 另外，HttpServletRequest 和 HttpServletResponse 也可以通过上面的方法来获取

## 注意

不要使用 `ModelAttribute` 注解来获取 HttpServletRequest 、HttpServletResponse  和 HttpSession

```java
protected HttpServletRequest request;
protected HttpServletResponse response;
protected HttpSession session;

@ModelAttribute
public void setReqAndRes(HttpServletRequest request, HttpServletResponse response) {
    this.request = request;
    this.response = response;
    this.session = request.getSession();
}


@PostMapping(value = "/msg1")
@ApiOperation("获取用户信息")
public GlobalResult msg1(){
    UserMsgResp userMsg = (UserMsgResp) session.getAttribute("userMsg");
    return GlobalResult.success(userMsg);
}
```

因为会产生线程不安全问题，所以不推荐使用