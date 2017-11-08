# JavaBean典型错误

---

昨天在学习JavaBean时，遇到各种问题，甚为恼火。下面稍微记录下：

- 错误一：`Unable to compile class for JSP:`不能编译`jsp`
出现这个错误的原因就是`JavaBean`放在了裸体类中，没有使用`package`包裹一层；

- 错误二:` org.apache.jasper.JasperException: java.lang.ClassNotFoundException: org.apache.jsp.ch7.ex7_002d1_jsp`类找不到错误
出现这个错误，的确很奇葩。首先明确一点，`JavaBean`类已经使用`package`打包，但还是出现了错误。可能的原因是：
```
<jsp:useBean id="myTriangle" type="warp.Triangle" scope="page"/>
这句话乍一看 没问题，但其实我们少写了一个东西。
<jsp:useBean id="myTriangle" class="wrap.Triangle" type="wrap.Triangle" scope="page"/>
type可以不指定，但是class必须指定。
```
 
 




