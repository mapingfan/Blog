# HTML学习记录

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8">
    <title>Title</title>
</head>
<!-- 注意是frameset，并且属性是rows/cols -->
<!-- 这两个标签虽然已经废弃，但是还挺好用，可以嵌套划分页面框架。 -->
<frameset rows="20%,*">
    <frame src="top.html">
    <frameset cols="20%,*">
        <frame src="left.html">
        <frame name="right">
    </frameset>
</frameset>
</html>
```
