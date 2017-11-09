# Servlet/JSP中的四大生存周期

标签（空格分隔）： jsp

---

在学习`JSP`时，肯定是避不开内置对象的，如`request，session，application`等。有时候我对这些对象的生命周期还是很好奇的。对于他们的大致区别我能辨别，但是总感觉有一丝模糊，所以这个地方查些资料，总结下。
这篇文章主要是讲内置隐式对象的作用域，也可以理解为他们的生存周期。
内容有如下四个点：

 1. `application`
 2. `session`
 3. `request`
 4. `page`
下面对每个对象总结下：

---

- `application/context`对象作用域
这个对象的生存周期始于我们的`web`应用运行时，结束于`web`应用结束或者重启服务器（可以理解为Tomcat服务器运行和关闭）。这个对象里面保存的参数，属性，对于所有的请求（`request`）和会话（`session`）都是可以获得的。在`servlet`程序中，我们可以通过直接在`servlet`代码中调用`getServletContext`获得`application`对象，也可以显示调用`getServletConfig().getServletContext()`。这个对象活的时间是相当的长。

- `session`对象作用域
始于一个客户端（例如浏览器窗口）同`web`应用建立连接，结束于浏览器窗口被关闭。一个`session`可以横跨一个客户端的多个请求。
对于`标签式`浏览器，`session`是共享的
- `request`对象作用域
始于发起请求，结束于返回响应。也可以这样理解，从调用`service方法`，到`service`方法结束。对于同一个请求，`request`是共享的。要区分重定向和转发。
- `page`对象作用域
只对创建这个对象的页面有效，出了页面就无效。

从上倒下，生存周期逐渐变短。
[参考文档][1]
 


  [1]: http://www.javajee.com/application-request-session-and-page-scopes-in-servlets-and-jsps