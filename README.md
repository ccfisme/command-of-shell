* 关于PATH的作用： 
> PATH说简单点就是一个字符串变量，当输入命令的时候LINUX会去查找PATH里面记录的路径。比如在根目录/下可以输入命令ls,在/usr目录下也可以输入ls,但其实ls这个命令根本不在这个两个目录下，事实上当你输入命令的时候LINUX会去/bin,/usr/bin,/sbin等目录下面去找你此时输入的命令，而PATH的值恰恰就是/bin:/sbin:/usr/bin:……。其中的冒号使目录与目录之间隔开。可以在脑中想一想平时打开文件的目录的样子。
* 关于新增自定义路径： 
现在假设你新安装了一个命令在`/usr/locar/new/bin`下面，而你又想像ls一样在任何地方都使用这个命令，你就需要修改环境变量PATH了，准确的说就是给PATH增加一个值`/usr/locar/new/bin`。你只需要一行bash命令`export PATH=$PATH:/usr/locar/new/bin`。这条命令的意思太清楚不过了，使PATH自增:`/usr/locar/new/bin`,即
`PATH=PATH+":/usr/locar/new/bin"`;通常的做法是把这行bash命令写到`/root/.bashrc`的末尾，然后当你重新登陆LINUX的时候（应该是linux启动时就会执行这个文件），新的默认路径就添加进去了。当然这里你直接用`source /root/.bashrc`执行这个文件重新登陆了。你可以用`echo $PAT命令查看PATH的值。
* 关于删除自定义路径： 
> 当某天你发现你新增的路径/usr/locar/new/bin已经没用了的话，你可以修改/root/.bashrc文件里面你新增的路径。或者你可以修改/etc/profile文件删除你不需要的路径  
  
# Linux中的环境变量  

* 引言   
>     在 linux系统 下，如果你下载并安装了应用程序，很有可能在键入它的名称时出现“ command not found ”的提示内容。如果每次都到安装目标文件夹内，找到可执行文件来进行操作就太繁琐了。这涉及到环境变量 PATH 的设置问题，而 PATH 的设置也是在 linux 下定制环境变量的一个组成部分。本文基于 RedHat 9.0 ，详细讲解了环境变量定制的问题。
  
* 变量简介  
 
>     Linux 是一个多用户的操作系统。每个用户登录系统后，都会有一个专用的运行环境。通常每个用户默认的环境都是相同的，这个默认环境实际上就是一组环境变量的定义。用户可以对自己的运行环境进行定制，其方法就是修改相应的系统环境变量。
  
* 定制环境变量   
>    环境变量是和 Shell 紧密相关的，用户登录系统后就启动了一个 Shell 。对于 Linux 来说一般是 bash ，但也可以重新设定或切换到其它的 Shell 。根据发行版本的情况， bash 有两个基本的系统级配置文件： /etc/bashrc 和 /etc/profile 。这些配置文件包含两组不同的变量： shell 变量和环境变量。前者只是在特定的 shell 中固定（如 bash ），后者在不同 shell 中固定。很明显， shell 变量是局部的，而环境变量是全局的。环境变量是通过 Shell 命令来设置的，设置好的环境变量又可以被所有当前用户所运行的程序所使用。对于 bash 这个 Shell 程序来说，可以通过变量名来访问相应的环境变量，通过 export 来设置环境变量。下面通过几个实例来说明。  
    
 >    1、 使用命令echo 显示环境变量  
    
    
```
    #本例使用echo显示常见的变量HOME   
    $ echo $HOME   
    /home/lqm   
```
  
 >    2、 设置一个新的环境变量   
      
```
    $ export HELLO=“Hello!”   
    $ echo $HELLO  
     Hello!   
```  

    
 >    3、 使用 env 命令显示所有的环境变量   
     
           
```
    $ env   
    SSH_AGENT_PID=1875   
    HOSTNAME=lqm   
    SHELL=/bin/bash   
    TERM=xterm   
    HISTSIZE=1000   
```  


       
 >    4、 使用 set 命令显示所有本地定义的 Shell 变量   
     
           
```
    $ set   
    BASH=/bin/bash  
```
       
 >    5、  使用 unset 命令来清除环境变量   
       
```
    $ export TEST=“test”       
    # 增加一个环境变量 TEST   
    $ env | grep TEST            
    # 此命令有输出，证明环境变量 TEST 已经存在了   
    TEST=test   
    $ unset $TEST 
    #删除环境变量TEST   
    $ env | grep TEST           
    # 此命令无输出，证明环境变量 TEST 已经存在了
```
      
 >    6、  使用 readonly 命令设置只读变量   
    
    如果使用了 readonly 命令的话，变量就不可以被修改或清除了。示例如下：   
       
```
    $ export TEST="Test..."                                        
    # 增加一个环境变量 TEST   
    $ readonly TEST 
    #将环境变量TEST设为只读   
    $ unset TEST 
    #会发现此变量不能被删除   
    -bash: unset: TEST: cannot unset: readonly variable   
    $ TEST="New" 
    #会发现此变量不能被修改   
    -bash: TEST: readonly variable   
```
      
 
 >    7、  用 C 程序来访问和设置环境变量   
    对于 C 程序的用户来说，可以使用下列三个函数来设置或访问一个环境变量。
  
    getenv() 访问一个环境变量。输入参数是需要访问的变量名字，返回值是一个字符串。如果所访问的环境变量不存在，则会返回 NULL 。
  
    setenv() 在程序里面设置某个环境变量的函数。
  
    unsetenv() 清除某个特定的环境变量的函数。
  
    另外，还有一个指针变量 environ ，它指向的是包含所有的环境变量的一个列表。下面的程序可以打印出当前运行环境里面的所有环境变量：   
       
```
    #include    
    extern char**environ;   
    int main ()       
    {   
        char**var;   
        for (var =environ;*var !=NULL;++var)   
        printf ("%s /n ",*var);   
        return 0;       
    } 
```
       
 >    8、 通过修改环境变量定义文件来修改环境变量。  
    
  
    需要注意的是，一般情况下，这仅仅对于普通用户适用，避免修改根用户的环境定义文件，因为那样可能会造成潜在的危险。  
    
  
       
```
    $cd #到用户根目录下   
    $ls -a                                  
    # 查看所有文件，包含隐藏的文件   
    $vi .bash_profile                   
    # 修改环境变量定义文件
    
```
       
    然后编辑你的 PATH 声明，其格式为：   
    
```
    PATH=$PATH::::------:   
```
    你可以自己加上指定的路径，中间用冒号隔开。环境变量更改后，在用户下次登陆时生效，如果想立刻生效，则可执行下面的语句：`$ source .bash_profile  ` 
    需要注意的是，最好不要把当前路径 `./` 放到 PATH 里，这样可能会受到意想不到的攻击。完成后，可以通过` $ echo $PATH` 查看当前的搜索路径。这样定制后，就可以避免频繁的启动位于 shell 搜索的路径之外的程序了。
  
* 总结   
>    通过以上的设置，你可以有一个比较方便有效的环境来提高你的工作效率了。

参考：https://wenku.baidu.com/view/ba4c5400f7ec4afe04a1dfd0.html
