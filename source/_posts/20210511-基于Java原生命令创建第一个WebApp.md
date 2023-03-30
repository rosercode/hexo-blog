---
title: java | 基于java原生命令创建第一个WebApp
date: 2021-05-11
tags:


---

使用原生命令来构建第一个 Web App

<!-- more --> 



## 前言

## 环境

## 为什么

为什么要使用原生命令来构建第一个 Web App

使用 IDE 来创建 Web 应用程序是一个非常方便的方法，它可以帮助开发人员更快速、更高效地开发应用程序。但是，了解如何使用 Java 原生命令来构建 Web 应用程序也是非常重要的。这是因为在某些情况下，你可能需要在没有 IDE 的情况下进行开发，或者你可能需要对构建过程进行更精细的控制和定制。此外，了解如何使用原生命令构建 Web 应用程序还有助于开发人员更好地理解应用程序的内部机制和原理，使他们成为更有技能的开发人员。因此，学习使用原生命令来构建 Web 应用程序是非常值得的。

## 构建

### 创建项目

在本地计算机上创建一个项目目录，用于存放 Java 源代码和编译后的类文件

```bash
mkdir my-web-app
cd my-web-app
```

### 编写 Servlet 类

```java
import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

@WebServlet("/hello")
public class MyServlet extends HttpServlet {

   public void doGet(HttpServletRequest request, HttpServletResponse response)
      throws ServletException, IOException {
      
      response.setContentType("text/html");
      PrintWriter out = response.getWriter();
      out.println("<html>");
      out.println("<head>");
      out.println("<title>Hello World Servlet</title>");
      out.println("</head>");
      out.println("<body>");
      out.println("<h1>Hello World from a Servlet!</h1>");
      out.println("</body>");
      out.println("</html>");
   }
}

```

### 编译 Java 类文件

```bash
javac -cp "servlet-api.jar" MyServlet.java
```

其中，-cp 参数指定了类路径，即 servlet-api.jar 文件的位置。servlet-api.jar 文件是 Java Servlet API 的库文件，它包含了 HttpServlet 类和其他 Java Servlet API 类。

### 创建 war 文件	

创建 WAR 文件：使用以下命令将 MyServlet.class 文件打包成一个名为 mywebapp.war 的 WAR 文件：

```bash
jar cvf mywebapp.war MyServlet.class
```

### 部署 war 文件

将 mywebapp.war 文件复制到 Web 服务器的 webapps 目录中，然后启动 Web 服务器。

### 访问 Web 应用程序

启动 Web 服务器，并使用 Web 浏览器访问 Web 应用程序。在浏览器中输入 URL 地址（如“http://localhost:8080/mywebapp/hello”），其中“localhost”是 Web 服务器的主机名，“8080”是 Web 服务器的端口