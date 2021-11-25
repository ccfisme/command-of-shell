之前编辑文件后执行时，有时候是用`./a.out`，有时候是`source .bash_profile`，有时候是`source ./project`，不明白为什么会有这么多的执行命令，所以准备探索其中的异同。  

首先，先要搞清楚而一点是，这所有的区别可以总结为`./文件`  与   `. ./文件`和`. 文件`的区别，而造成前两者区别的原因是在Mac的script脚本里都有一句`#! /bin/bash`，这个的意思是当前终端所在的shell fork一个子shell（详见http://xstarcd.github.io/wiki/shell/fork_exec_source.html ）然后执行文件，执行完了再返回终端所在的shell。 


所以，目的就明确了。探索的目的是探究父shell与子shell之间的联系  

先编辑一个ccf1.sh  

![image](https://user-images.githubusercontent.com/74129445/143374764-1b32a55a-ba2d-489b-a0db-b65110834913.png)  

然后分别运行`./ccf1.sh`  与   `. ./ccf1.sh`  


![image](https://user-images.githubusercontent.com/74129445/143374713-825e4452-e513-4e38-aadf-44b791d9052c.png)  

由图可以看出,由'./'运行子进程遭到了访问权限的拒绝，也就是申请进程失败，而'. ./'由于是在当前进程运行，所以可以执行出结果  



参考：https://www.cnblogs.com/cangqinglang/p/11085013.html


















































