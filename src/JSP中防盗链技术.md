# JSP中防盗链技术

标签（空格分隔）： JSP

---

今天偶然学习到一个知识点，利用`referer`和`response.setStatus(404);`防止盗链。
如果我们从`A`页面的超链接访问`B`页面，这时候，我们可以在`B`页面通过`String referer = request.getHeader("referer");`获取`referer`，这个`referer`的值就是`A`页面的`url`值。在`B`页面，通过检测`referer`值，可以进行访问控制。从而达到访问控制技术。




