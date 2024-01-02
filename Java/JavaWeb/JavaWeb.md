## web项目是如何运行的？

web项目包含前端代码和后端代码，前端代码都是一些静态的资源包括html，css，图片资源等，这些资源可以直接放到浏览器中，浏览就能直接解析这些资源，但是后端资源如何运行呢？后端资源主要就是后端的代码，运行这些代码需要使用服务器，通过服务器的解析才能拿到后端的数据最终和前端相结合生成一个web网站。目前后端主流的编程语言是Java，下面将介绍如何使用Java语言和前端配合开发web网站

## Tomcat作为web的运行环境

后端项目的运行环境包括哪些呢？目前主流的包括NGINX和Tomcat两款，目前我们在Windows系统学习和演示主要使用的是Tomcat，之后在Linux系统中使用NGINX居多，因为NGINX功能更加的强大而且更加轻量，后期也会针对NGINX做单独的学习

[NGINX](https://www.nginx.com/)

[Apache Tomcat® - Welcome!](https://tomcat.apache.org/)

### 如何安装Tomcat

打开Tomcat的官网可以看到目前主流的Tomcat版本，虽然目前企业中使用的大多数还是Tomcat8之类的，但是迟早有一天会提升版本，目前我们演示的话就使用最新版本的Tomcat10

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704174081542-ca20145b-ccfc-4c5a-98d6-b1f1b84493bd.png)

点击压缩包进行下载解压之后就能获得Tomcat最新的版本，无需再次安装，个人感觉这样方便一些。

接下来就是如何使用Tomcat了，在使用之前我们需要先配置本地的Java开发环境，确保你的系统已经配置jdk11及其以上的Java开发环境。可以使用`java-versaion`命令检查。

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704174264817-97564719-40ca-439e-9de6-d60983fcaa7a.png)

现在我们就可以开始使用Tomcat了，在使用Tomcat之前我们有必要先来了解一下目录结构

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704174363469-dce5ddf8-a6b0-441e-ae84-f3decf459168.png)

bin目录：

主要是用来存放tomcat的命令，主要有两大类，一类是以.sh结尾的（linux命令），另一类是以.bat结尾的（windows命令）。很多环境变量的设置都在此处，例如可以设置JDK路径、tomcat路径，startup 用来启动tomcat，shutdown 用来关闭tomcat，修改catalina可以设置tomcat的内存。

conf目录：

conf目录主要是用来存放tomcat的一些配置文件。server.xml可以设置端口号、设置域名或IP、默认加载的项目、请求编码web.xml可以设置tomcat支持的文件类型，context.xml可以用来配置数据源之类的，tomcat-users.xml用来配置管理tomcat的用户与权限，在Catalina目录下可以设置默认加载的项目。

lib目录：

主要用来存放tomcat运行需要加载的jar包。例如，像连接数据库的jdbc的包我们可以加入到lib目录中来。因为Tomcat本身也是Java程序开发的，故需要jar包的支持。

logs目录：

logs目录用来存放tomcat在运行过程中产生的日志文件，非常重要的是在控制台输出的日志。（清空不会对tomcat运行带来影响），在windows环境中，控制台的输出日志在catalina.xxxx-xx-xx.log文件中，在linux环境中，控制台的输出日志在catalina.out文件中。

temp目录：

temp目录用户存放tomcat在运行过程中产生的临时文件。（清空不会对tomcat运行带来影响）。

webapps目录：

webapps目录用来存放应用程序，当tomcat启动时会去加载webapps目录下的应用程序。可以以文件夹、war包、jar包的形式发布应用。当然，你也可以把应用程序放置在磁盘的任意位置，在配置文件中映射好就行。

work目录:

work目录用来存放tomcat在运行时的编译后文件，例如JSP编译后的文件。清空work目录，然后重启tomcat，可以达到清除缓存的作用。~

### 启动Tomcat

就像上面所说的那样，在Windows系统中只要点击startup.bat文件就能在控制台启动Tomcat，此时我们就可以在浏览器中输入127.0.0.1:端口/项目名称，就可以访问对应的项目，Tomcat中给我们提供了几个项目，只要输入对应的文件夹名称就可以进行访问。

有的时候Tomcat启动的时候在控制台上会出现乱码，因为可能此时我们的设备使用的是gbk编码而Tomcat使用的是utf-8编码此时我们只需要去配置文件中找到对应的编码配置修改即可。

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704175095502-fcfe5434-cbc1-46d2-bd01-bcb318df45de.png)

当然我们也可以修改访问的端口号以及在URL中的项目名称，注意：上下文路径是可以进行修改的并不是说一定需要使用和文件名称一样的上下文路径访问对应的项目。由于之后我们需要再idea中配置Tomcat，在那里将会有更方便的方式更改上下文路径。

## 在IDEA中开发WEB项目

第一步将Tomcat集成到idea中

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704176119472-569eb141-e06b-4932-94a3-1b254b8f8f5a.gif)

### 创建web项目

由于在idea中直接创建的项目并不属于web项目所以我们需要手动的为创建的项目添加web模块，在旧版的idea中可以直接右键找到addframework就可以找到添加的地方，在新版本中需要打开项目设置然后在其中添加web模块，其中在添加web.xml文件的时候需要选择5.0及其以上的版本，因为我们使用的是Tomcat10，在添加完成之后需要在web包下创建对应的模块

其中static是存放静态资源文件的，在WEBINF中添加lib包，再将lib包添加为模块依赖，之后如果我们想在项目中添加MySQL等的jar包的时候就可以直接放在lib目录下面，这样我们的一个简单的web项目的基础框架就搭建完成了。

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704176693926-810d577a-a104-43ff-9450-bbeb2233269d.gif)

在实现第一个web项目之前我们先来了解一下idea是如何部署web项目的。

难道我们将Tomcat和idea联合在一起idea就一定将项目部署到Tomcat中的webAPP里面了吗？其实不然，idea是将build之后的项目部署在了Tomcat的一个副本中，我们可以看一下

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704177003752-cdb87fe7-333a-420d-9b96-6b7ea54aa496.png)

当我们点击build之后idea就将项目打包成为一个web项目，并将其输出放在out目录下面，我们可以看一下之前Tomcat中是否存在一个同名的文件：

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704177093249-60ec79af-2e18-438a-a9f0-9add3913387b.png)

可以看到还是之前的几个文件并不存在我们当前build的文件，那idea是如何将项目部署起来的呢？

我们看一下控制台可以发现：

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704177201339-ffee8ab4-41ef-4e12-8c3e-be41b914c8e9.png)

idea自动生成了一个Tomcat的副本

打开副本：

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704177267527-217b001c-a690-4f2c-b5f4-9f5206471fa4.png)

其中第一个文件夹下面存在一个和打包之后项目同名的配置文件，打开配置文件中后发现

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704177327568-71c7e454-83e0-4d35-a29d-7d5d34b20624.png)

其中正好是记录了我们打包之后项目的存放路径，从这可以推断出，其实idea是为每一个web项目都创建了单独的配置文件，然后配置文件中记录了当前项目的存放路径，之后就可以直接找到项目并运行项目了。

## servlet简介

Java Servlet 是运行在 Web 服务器或应用服务器上的程序，它是作为来自 Web 浏览器或其他 HTTP 客户端的请求和 HTTP 服务器上的数据库或应用程序之间的中间层。

使用 Servlet，您可以收集来自网页表单的用户输入，呈现来自数据库或者其他源的记录，还可以动态创建网页。

Java Servlet 通常情况下与使用 CGI（Common Gateway Interface，公共网关接口）实现的程序可以达到异曲同工的效果。但是相比于 CGI，Servlet 有以下几点优势：

- 性能明显更好。
- Servlet 在 Web 服务器的地址空间内执行。这样它就没有必要再创建一个单独的进程来处理每个客户端请求。
- Servlet 是独立于平台的，因为它们是用 Java 编写的。
- 服务器上的 Java 安全管理器执行了一系列限制，以保护服务器计算机上的资源。因此，Servlet 是可信的。
- Java 类库的全部功能对 Servlet 来说都是可用的。它可以通过 sockets 和 RMI 机制与 applets、数据库或其他软件进行交互。

### Tomcat是如何调用servlet的

- 浏览器（客户端）向服务器端发送请求，请求中保存着各种数据
- Tomcat收到请求之后将收到的数据转换成一个HttpServletRequest对象，同时生成一个HttpServletResponse对象
- 目前Tomcat仍然不知道接下来收到的数据如何处理，这个时候我们就需要指定Java的类去实现这个功能，当然我们也不能按照我们自己的标准来搞，这样就混乱了，此时Tomcat将会给我们提供一个接口（规范），然后我们去实现这个接口中的方法
- 然后我们就可以在我们编写的类中处理Tomcat提供的数据了，处理完成之后将数据返回给Tomcat，Tomcat将数据返回给浏览器，此时就完成了整个访问。

### 如何开发一个servlet项目

首先我们需要创建一个Java类以此来实现业务方法。但是Tomcat给出了规定，故我们需要实现servlet方法，然后在其中实现我们的业务方法，但是servlet给我们提供了很多的方法，现阶段我们并不需要所有都使用，故在实现这个方法的时候可以直接继承HttpServlet类然后实现其中的方法

```java
package cn.rlfit.servlet;

import jakarta.servlet.ServletException;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

/**
 * 创建JavaWeb项目，将Tomcat添加为当前项目的依赖
 * 以上类都是Tomcat提供的
 * 重写service方法
 * 在service中定义业务方法
 * 在web.xml中配置servlet对应的请求路径
 */
public class UserServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//        可以从请求中获取请求的任意参数
        String username = req.getParameter("username");
        if ("rlfit".equals(username)){
            resp.getWriter().write("No");
        }else {
            resp.setHeader("Content-Type", "text/html");
            resp.getWriter().write("<h1>Yes</h1>");
        }
//        处理业务代码
//        将响应数据放入resp
    }
}
```

req和resp是核心，当中提供了很多的方法给我们使用。我们实现了上述代码之后还需要在指定我们如何才能访问这个类，此时就需要再配置文件中提供对应的配置文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd"
         version="6.0">
<!--    配置servlet类，起一个别名-->


    <servlet>
        <servlet-name>userServlet</servlet-name>
        <servlet-class>cn.rlfit.servlet.UserServlet</servlet-class>
    </servlet>
    <servlet-mapping>
        <servlet-name>userServlet</servlet-name>
        <url-pattern>/userServlet</url-pattern>
    </servlet-mapping>
</web-app>
```

对应的前端代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<form action="userServlet" method="get">
    <h1>校验用户名</h1>
    <input type="text" name="username"><br>
    <input type="submit" value="校验">
</form>
</body>
</html>
```

当我们启动项目在页面上输入数据的时候前端就自动将数据传递给后端然后后端通过xml配置文件找到`<url-pattern>/userServlet</url-pattern>`，通过这找到`<servlet-name>userServlet</servlet-name>`，通过这找到`<servlet-class>cn.rlfit.servlet.UserServlet</servlet-class>`，然后通过反射技术加载对应的类实现对应的方法， 当然一个类可以对应多个pattern和多个mapping，并且在书写pattern的时候我们可以使用通配符的方式来来书写

/表示可以匹配所有，但是不能匹配jsp，/*表示可以匹配连通jsp在内的所有/a/*表示匹配a开头的所有，/*.a表示匹配以a为后缀的所有，当然还有更简单的注释方式实现上述效果，接下来将会演示。

## Servlet-api.jar和Content-Type注意事项

都知道Java本身的API并不会携带Servlet-api.jar，那么我们在使用的时候应该如何导入对应的jar包呢？在使用的时候直接将Tomcat携带的依赖添加进Java项目中，也可以使用lib的方式将servlet-api.jar添加进入，但是当我们使用后者进行添加的时候需要将scop的值设置为private，不要设置成为compile。不然会造成jar包的 冲突

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704178290213-119756db-59cd-42e2-8442-046b4aa6bf98.png)

在项目中一定要设置Content-Type的类型，如果不设置默然会匹配文件后缀对应的类型，但是在servlet中没有文件后缀，会默认使用txt/html的方式进行解析，但是如果我们不设置的话如果是其他文件，可能会出现访问错误的问题。

## 注解的方式开发Servlet

使用注解的方式开发servlet的话将会更加的方便，使用注解的方式将不需要在配置.xml文件，

```java
package cn.rlfit.servlet;

import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

/**
 * 创建JavaWeb项目，将Tomcat添加为当前项目的依赖
 * 以上类都是Tomcat提供的
 * 重写service方法
 * 在service中定义业务方法
 * 在web.xml中配置servlet对应的请求路径
 */
@WebServlet("/userServlet")
public class UserServlet extends HttpServlet {
    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
//        可以从请求中获取请求的任意参数
        String username = req.getParameter("username");
        if ("rlfit".equals(username)){
            resp.getWriter().write("No");
        }else {
            resp.setHeader("Content-Type", "text/html");
            resp.getWriter().write("<h1>Yes</h1>");
        }
//        处理业务代码
//        将响应数据放入resp
    }
}
```

在WebServlet中存在多个值

```java
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

package jakarta.servlet.annotation;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface WebServlet {
    // name属性是单独配置一个值时使用的
    String name() default "";
// 配置多个值时使用的
    String[] value() default {};

    String[] urlPatterns() default {};

    int loadOnStartup() default -1;

    WebInitParam[] initParams() default {};

    boolean asyncSupported() default false;

    String smallIcon() default "";

    String largeIcon() default "";

    String description() default "";

    String displayName() default "";
}
```

## Servlet生命周期

我们在第一次实现自己的servlet类的时候是直接实现servlet的那个时候后需要我们直接实现好几个方法，我们来看一下servlet接口中定义的方法

```java
//
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//

package jakarta.servlet;

import java.io.IOException;

public interface Servlet {
    void init(ServletConfig var1) throws ServletException;

    ServletConfig getServletConfig();

    void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;

    String getServletInfo();

    void destroy();
}
```

可以发现里面有初始化方法，服务方法，和销毁方法，servlet在执行的时候都会依次执行上述方法，这就是servlet的生命周期，那么什么时候执行对应的方法呢？我们可以在自己的servlet中重写上述方法来看看

```java
package cn.rlfit.servlet;

import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

import java.io.IOException;

/**
 * 创建JavaWeb项目，将Tomcat添加为当前项目的依赖
 * 以上类都是Tomcat提供的
 * 重写service方法
 * 在service中定义业务方法
 * 在web.xml中配置servlet对应的请求路径
 */
@WebServlet({"/userServlet"})
public class UserServlet extends HttpServlet {
    public UserServlet() {
        System.out.println("构造方法执行");
    }

    @Override
    public void init() throws ServletException {
        System.out.println("初始化方法执行");
    }

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        System.out.println("服务方法执行");
//        可以从请求中获取请求的任意参数
        String username = req.getParameter("username");
        if ("rlfit".equals(username)) {
            resp.getWriter().write("No");
        } else {
            resp.setHeader("Content-Type", "text/html");
            resp.getWriter().write("<h1>Yes</h1>");
        }
//        处理业务代码
//        将响应数据放入resp
    }

    @Override
    public void destroy() {
        System.out.println("销毁方法执行");
    }
}
```

![img](C:\Users\18777\Desktop\note\Java\JavaWeb\JavaWeb\1704187679293-24431b5d-2af6-4aaa-9a47-b19457eeec0b.gif)

可以发现当我们在页面中点击校验的时候控制台上打印出了几个方法的执行顺序，当我们点击销毁的时候控制台上也打印出了销毁方法被执行，可以说明servlet的生命周期方法是在我们使用servlet方法的时候执行的，并且在继续点击校验的时候只会执行service方法，说明初始化和构造器方法都只会执行一次。

那么是不是就只能在我们使用的时候执行初始化方法呢？其实也可以在我们启动项目的时候就先执行，这样用户在访问的时候可以提高一些访问的速度，具体的我们可以在.xml文件中配置loadOnStartup的值为一个正整数，因为这个字段的值默认是-1，配置之后就可以在启动的时候加载完成，当然也可以使用注解的方式进行配置，我们不建议将这个字段的值设置为10以内的数字，因为Tomcat存在默认的.xml文件，其中可能已经配置了对应的字段

DefaultServlet，这是Tomcat提供的默认处理静态资源的Servlet，其实我们页面中的所有请求在Web项目中都是需要通过servlet方法去处理的，其中的静态资源就是利用上述的默认方法进行处理的。这个方法在讲解springMVC的时候还会详细解释.

还要注意的一点是不建议在service方法中修改变量（使用共享变量），这会造成线程的不安全问题。

## servlet继承结构



## 参考：

https://blog.csdn.net/u012661010/article/details/73381599

https://www.runoob.com/servlet/servlet-intro.html