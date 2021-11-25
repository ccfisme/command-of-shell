chmod命令，全称Change Mode  

## 包含字母和操作符表达式的文字设定法 

其语法格式为：`chmod [who] [opt] [mode] 文件/目录名 `  

* who表示对象，是以下字母中的一个或组合： 
```
u：表示文件所有者 
g：表示同组用户 
o：表示其它用户 
a：表示所有用户 
```  

* opt则是代表操作，可以为： 
```
+：添加某个权限 
-：取消某个权限 
=：赋予给定的权限，并取消原有的权限 
```  

* 而mode则代表权限： 
```
r：可读 
w：可写 
x：可执行 

```  

例如：为同组用户增加对文件a.txt的读写权限： 

`chmod g+rw a.txt `  

## 用数字设定法   


语法格式为：`：chmod [mode] 文件名 `  

![image](https://user-images.githubusercontent.com/74129445/143348024-547bcadd-f587-497a-a90f-5009805dd040.png)  
参考：https://blog.csdn.net/ULi_cloud/article/details/73187469














































