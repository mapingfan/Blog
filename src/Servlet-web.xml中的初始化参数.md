# Servlet/web.xml中的初始化参数

标签（空格分隔）： jsp

---

`init-param`与`context-param`
```
<context-param>
        <param-name>school</param-name>
        <param-value>whu</param-value>
    </context-param>
```
这些标记是`web-app`的直接子标记。所有依赖这个`web.xml`文件的`Servlet、jsp`都能读取的。如果想指定某个`servlet`读取一些初始化参数，那么写下如下子标记：
```
<servlet>
        <servlet-name>testInitParam</servlet-name>
        <servlet-class>handle.TestInitParam</servlet-class>
        <init-param>
            <param-name>p1</param-name>
            <param-value>p111</param-value>
        </init-param>
        <init-param>
            <param-name>p2</param-name>
            <param-value>p2222</param-value>
        </init-param>
    </servlet>
```
也就是写成某个具体`Servlet`的子标记。
我们在文件中可以这样访问：
```
out.println(this.getServletConfig().getInitParameter("p1"));
        out.println(this.getInitParameter("p1"));
        out.println(this.getInitParameter("p2"));
        out.println(this.getServletConfig().getServletContext().getInitParameter("school"));
        out.println(this.getServletContext().getInitParameter("school"));

```
上面是在`Servlet`中访问的，下面是在`jsp`中访问：
```
<%=config.getServletContext().getInitParameter("school")%>
主要是通过内置的隐式config对象来获取这些参数。
```




