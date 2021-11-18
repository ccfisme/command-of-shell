首先，先介绍[.inputrc在打开终端的初始化起到的作用]()

然后，就是设置.inputrc  


* 第一步，打开终端，输入`vi .inputrc`  



* 第二步，在.inputrc可以进行输入格式的修改  


![image](https://user-images.githubusercontent.com/74129445/142347359-479f342b-c1e5-42a4-9021-9f3b4ec1aefb.png)  



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

