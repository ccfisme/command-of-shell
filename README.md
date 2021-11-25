# javac命令行  

javac用于编译java源文件，生成.class文件。形式如下`javac [option] source`  

例：  

![image](https://user-images.githubusercontent.com/74129445/143484882-068e9da1-a11d-4f72-ad50-4ad7cbdcc260.png)  

javac 新建shell运行源java文件变为class文件并通过-d链接到目标目录下的新建shell  



# 2.java命令行  

java用于运行.class文件。形式如下：`java [option] classname [arguments]`  

其中，Java后面的最终文件不能含有.class，否则会报错  

例：  


![image](https://user-images.githubusercontent.com/74129445/143438706-955f91d2-bf69-46c1-ba55-177586bded16.png)  

当没包时，可以直接在当前文件java 类名；当有包时，需要用-cp命令来链接到包下的class文件去执行  

java 通过-cp命令链接到包下的class文件然后执行

参考：  
* https://github.com/ccfisme/JAVA/tree/Java%E5%9C%A8%E7%BB%88%E7%AB%AF%E4%B8%AD%E7%9A%84%E8%BF%90%E8%A1%8C%E5%91%BD%E4%BB%A4  

* https://www.jianshu.com/p/033dcc32e8cd  

* http://docs.linuxtone.org/ebooks/C&CPP/c/ch31s03.html

