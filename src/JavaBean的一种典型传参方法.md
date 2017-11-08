# JavaBean的一种典型传参方法

---

最近写`JavaBean`程序时，会遇到这种一种情况，利用表单的参数来修改`Bean`的值。这种做法十分简单，但是用处去很大。
下面看下例子
```
<%@ page contentType="text/html;charset=utf-8" language="java" %>
<jsp:useBean id="myShow" class="wrap.Show" type="wrap.Show" scope="session"/>
<html>
<head>
    <title>ShowPic</title>
</head>
<body>
<jsp:getProperty name="myShow" property="pic"/>
<jsp:setProperty name="myShow" property="cnt" param="num"/>
<form action="" method="post">
   <input type="hidden" name="num" value="<%=myShow.getCnt()-1%>">
    <input type="submit" value="上一张">
</form>
<form action="" method="post">
    <input type="hidden" name="num" value="<%=myShow.getCnt()+1%>">
    <input type="submit" value="下一张">
</form>
</body>
</html>

```

```
package wrap;

import java.io.File;

public class Show {
    private String pic;
    private String[] picStorage;
    private int cnt = 0;

    public int getCnt() {
        return cnt;
    }

    public void setCnt(int cnt) {
        if (cnt > 2) {
            cnt = 0;
        } else if (cnt < 0) {
            cnt = 2;
        }
        this.cnt = cnt;
    }

    public String getPic() {
        File file = new File("F:\\JavaWeb项目\\JSP实践\\web\\ch7\\ex7-3\\pic");
        picStorage = file.list(new MyFileNameFilter("jpg"));
        pic = "<img src=pic/"+picStorage[cnt]+ " width=100 height=100/>";
        return pic;
    }
}

```
在上面的例子中，我们的这句`<jsp:setProperty name="myShow" property="cnt" param="num"/>`，使用的是表单参数来赋值。这样有一个好处，就是即使我们的表单参数是空的，这样的修改也不会造成异常。如果我们用`request.getParameter()`方法来接收参数，总是要处理下参数值为`null`的异常。但是`JavaBean`中，我们不需要。
还有一点就是表单隐藏字段的使用。
当我们提交表单到另一个页面时，传递过去的参数，也可以直接使用`param`进行赋值，不需要先去取得参数，然后使用`value`进行赋值。
这种设计方法很巧妙，所以我牢牢理解并且记住。



