# Servlet抽取

标签（空格分隔）： servlet

---

随着`Servlet`的深入学习，我们发现每一个前端页面需要请求数据，都需求去请求相应的`servlet`。往往前端页面都很多，那么在写`servlet`时会发现名字都不好想了。
既然出现痛点，那么这里就是创新之处。前辈们已经帮我们总结处了方法，我要做的就是提炼总结，融会贯通。
```
package com.whu.base;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

@WebServlet(name = "Servlet4", urlPatterns = {"/BaseServlet"})
public class BaseServlet extends HttpServlet {
    @Override
    public void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String method = req.getParameter("method");
        if (method != null && method.trim().length() != 0) {
            try {
                Method myMethod = this.getClass().getMethod(method, HttpServletRequest.class, HttpServletResponse.class);
                myMethod.invoke(this, req, resp);
            } catch (NoSuchMethodException e) {
                e.printStackTrace();
            } catch (IllegalAccessException e) {
                e.printStackTrace();
            } catch (InvocationTargetException e) {
                e.printStackTrace();
            }
        }
    }
}

```

---

```
package com.whu.myservlet;

import com.whu.base.BaseServlet;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

@WebServlet(name = "Servlet5", urlPatterns = {"/myServlet"})
public class MyServlet extends BaseServlet {
    public void method_1(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        response.getWriter().write("Method_1调用");

    }

    public void method_2(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        response.setContentType("text/html;charset=utf-8");
        response.getWriter().write("Method_2调用");

    }

}

```

以后可以这样访问：`http://localhost:8080/myServlet?method=method_name`.通过这样的做法，实现了分流，建立一个`servlet`就好。其中注意一点，`method_1`等方法不能是`protected`，必须改为`public`。否则反射时会找不到方法。

EOF.


