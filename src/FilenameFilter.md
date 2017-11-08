# FilenameFilter
标签（空格分隔）： jsp

---

`Java`中的`FilenameFilter`学习
```
class FileEndwithJSP implements FilenameFilter {
        String string = null;

        public FileEndwithJSP(String string) {
            this.string = "." + string;
        }
        
        @Override
        public boolean accept(File dir, String name) {
            return name.endsWith(this.string);
        }
    }
```
我们可以在代码中这样用：
``` 
FileEndwithJSP fileEndwithJSP = new FileEndwithJSP("md");  //只要md结尾的文件；
    File file = new File("F:\\JavaWeb项目\\JSP实践\\web\\ch4");
    String[] files = file.list(fileEndwithJSP);  //传入筛选器
    for (int i = 0; i < files.length; i++) {
        out.println(files[i]);
    }
```




