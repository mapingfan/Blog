# JSP页面提交中文表单乱码解决方案

标签（空格分隔）： jsp

---

当提交的`form`中有中文值时，如果接收端不进行设置就会出现乱码。

---

- 注意一点：**从tomcat8.0开始，URIEncoding默认值不再是ISO8859-1，而变成了UTF-8。那么也就意味着，从tomcat8.0开始，get请求中的中文参数，不需要特殊处理了。**所以这个时候，表单使用`get`方式提交，接收端不需要转码，因为已经是`UTF-8`。

---

- 注意二点：**利用request.setCharacterEncoding("UTF-8");来设置Tomcat接收请求的编码格式，只对POST方式提交的数据有效，对GET方式提交的数据无效!**

从上面我们可以知道，`Tomcat8`以后，对于`get`方法提交的中文参数，接收端不需要多余处理，如设置`request.setCharacterEncoding("UTF-8");`，原因上面已经解释过。
但是对于`post`方法，`tomcat8`好像并没有设置，我拿电脑测试了下，发现接收端接受到的`request.getCharacterEncoding();`,输出后的值竟然是`null`。所以对于`post`方法，处理中文时，我们对发送过来的请求必须指定编码方式，如`request.setCharacterEncoding("utf-8");`。

稍微总结下，对于`Tomcat8`之后，`get`请求无需额外处理，`post`请求要进行额外处理。




