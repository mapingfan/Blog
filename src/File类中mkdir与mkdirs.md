# File类中mkdir与mkdirs

标签（空格分隔）： Java jsp

---

在`Java的File`类中，有两个函数`mkdir、mkdirs`。对于这两个函数，以前一直有点不清楚，今天正好遇到，解决。直接看例子。
```
<%@ page import="java.io.File" %>
<%@ page contentType="text/html;charset=utf-8" language="java" %>
<html>
<head>
    <title>Title</title>
</head>
<body>
<%
    File file = new File("D:\\JavaWeb项目\\JSP实践\\web\\ch5", "hhh");
    out.println(file.mkdir());
%>
</body>
</html>

```
注意，`D盘`中并没有`D:\\JavaWeb项目\\JSP实践\\web\\ch5`这些目录。如果这个时候你想在`D:\\JavaWeb项目\\JSP实践\\web\\ch5`目录下创建一个`hhh`目录，那么`mkdir`是无法做到的，普通的`JavaSE`中甚至会报异常（`jsp中不会报异常`）。但是当我们使用`mkdirs`方法，创建却是成功的。

所以：当使用`mkdir`时，需要保证上级目录存在，否则只能用`mkdirs`。




