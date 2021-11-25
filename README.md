之前编辑文件后执行时，有时候是用`./a.out`，有时候是`source .bash_profile`，有时候是`source ./project`，不明白为什么会有这么多的执行命令，所以准备探索其中的异同。  

首先，先要搞清楚而一点是，这所有的区别可以总结为`./文件`  与   `. ./文件`和`. 文件`的区别，而造成前两者区别的原因是在Mac的script脚本里都有一句`#! /bin/bash`，这个的意思是当前终端所在的shell要fork一个子shell（[fork](http://xstarcd.github.io/wiki/shell/fork_exec_source.html) ），然后执行文件，执行完了再返回终端所在的shell。 


所以，目的就明确了。探索的目的是探究父shell与子shell之间的联系  

先编辑一个ccf1.sh  

![image](https://user-images.githubusercontent.com/74129445/143374764-1b32a55a-ba2d-489b-a0db-b65110834913.png)  

然后分别运行`./ccf1.sh`  与   `. ./ccf1.sh`  


![image](https://user-images.githubusercontent.com/74129445/143374713-825e4452-e513-4e38-aadf-44b791d9052c.png)  

由图可以看出,由'./'运行子进程遭到了访问权限的拒绝，也就是申请进程失败，而'. ./'由于是在当前进程运行，所以可以执行出结果  

这里可以验证出`./`的确是申请一个新shell来运行进程；`. ./`是在当前shell运行进程  

当然，这里的验证比较模糊，比如，对于`./`在另一个进程里运行，那么是两者的环境变量调用在一起；还是创建新shell新环境变量，调用完就立即销毁？所以进行下面的验证  

重写ccf1.sh  

![image](https://user-images.githubusercontent.com/74129445/143377090-bf9bf100-4ffa-4bd9-9978-d5c21c21adf8.png)  

然后在另一个shell里分别用`./`和`. ./`调用ccf1.sh，通过显示其环境变量来判断是当前shell运行还是新建子shell运行  

新建ccf2.sh

![image](https://user-images.githubusercontent.com/74129445/143377419-c7e26814-a52c-4ed9-ad52-7eb4179308fb.png)  

运行(这里ccf2.sh的运行`./`或者`. ./`没有区别)：  

![image](https://user-images.githubusercontent.com/74129445/143377473-4f746156-11a6-4d3d-b46b-92a83faad423.png)  

什么都没有  

重写ccf2.sh  

![image](https://user-images.githubusercontent.com/74129445/143377534-47bfc5af-ed1e-4a1e-990f-9302d6f675a6.png)  

运行：  

![image](https://user-images.githubusercontent.com/74129445/143377580-96489454-9627-4f9d-976e-491361d59101.png)
出现结果  

结论：如果不用点命令的话，会另起shell进程，而启动这个进行的时候，它会建立自己的进程环境（暂且这么叫它吧），然后在这个进行结束的时候，它所建立的环境也随之被销毁。而且点命令就不一样了，它会把点命令所带的shell脚本里的所以内容带到当前的shell进程里，在本程序里，就是变量a了。




参考：https://www.cnblogs.com/cangqinglang/p/11085013.html


















































