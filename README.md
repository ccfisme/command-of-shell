首先，先介绍[.bash_profile在打开终端的过程起到的的作用](https://github.com/ccfisme/Mac-and-Linux-directory-structure/blob/%EF%BD%9E%E4%B8%8B%E7%9A%84bash_profile%E5%B9%B2%E4%BB%80%E4%B9%88%E7%94%A8%E7%9A%84%EF%BC%9F/README.md)

然后，就是设置.bash_profile  


* 第一步，打开终端，输入  

![image](https://user-images.githubusercontent.com/74129445/142339202-86d1b02d-6aeb-43b8-946d-3737fbc89798.png)  

* 第二步，在.bash_profile可以进行名字格式的修改 

在 export PS1="" 的引号之间，您可以添加[以下行来自定义您的终端提示](http://osxdaily.com/2006/12/11/how-to-customize-your-terminal-prompt/)：  


* \d - 当前日期
* \t - 当前时间
* \h – 主机名
* \# – 命令编号
* \u - 用户名
* \W - 当前工作目录（即：桌面/）
* \w - 具有完整路径的当前工作目录（即：/Users/Admin/Desktop/） 

我想要的是只显示完整路径的名字，所以输入`export PS1="\u@\h\w $ "`  

重新打开终端可以看到名字已经修改  

![image](https://user-images.githubusercontent.com/74129445/142339934-f188c0db-b86e-474b-bc1a-e1a4be600319.png)  

值得一提的是，.bash_profile文件是在/User/ccf下面的，可以用`pwd`命令查看。

![image](https://user-images.githubusercontent.com/74129445/142340106-e89ad684-8673-4d74-8b11-bc3011f24e63.png)

