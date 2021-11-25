之前编辑文件后执行时，有时候是用`./a.out`，有时候是`source .bash_profile`，有时候是`source ./project`，不明白为什么会有这么多的执行命令，所以准备探索其中的异同。  

首先，先要搞清楚而一点是，这所有的区别可以总结为`./`与`. ./`的区别，而造成这种区别的原因是因为
参考：https://www.cnblogs.com/cangqinglang/p/11085013.html
