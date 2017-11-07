# JSP内置对象小结

标签（空格分隔）： JSP

---

今天把`jsp`中重要的内置对象学习了一遍，下面稍微总结。
最重要的对象有如下几个:

- session
- request
- response
- application

其中`application`对象的生存周期是最长的，对整个web应用都是可见的；
其次就是`session`对象；
最好是`request`对象；
在`web`开发中，常用这些对象来存储信息，但是这并不是唯一的方法。据我现在所学，我们可以通过`tag`文件传递参数和返回对象。也可以直接在`jsp`地址后追加参数，如`www.xxx.jsp?name=aibilim&sex=male`。
总而言之，传递参数的方法有很多，但是必须考虑到安全性问题以及同步问题。上面提到的`application`对象，里面存储的数据对整个`web app`是可见，可能会出现数据不一致的问题，所以修改时要注意是否需要加上同步方法`synchronized`。





