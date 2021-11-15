# 关于PATH的作用：
> PATH说简单点就是一个字符串变量，当输入命令的时候LINUX会去查找PATH里面记录的路径。比如在根目录/下可以输入命令ls,在/usr目录下也可以输入ls,但其实ls这个命令根本不在这个两个目录下，事实上当你输入命令的时候LINUX会去/bin,/usr/bin,/sbin等目录下面去找你此时输入的命令，而PATH的值恰恰就是/bin:/sbin:/usr/bin:……。其中的冒号使目录与目录之间隔开。


# 关于新增自定义路径：
> 现在假设你新安装了一个命令在/usr/locar/new/bin下面，而你又想像ls一样在任何地方都使用这个命令，你就需要修改环境变量PATH了，准确的说就是给PATH增加一个值/usr/locar/new/bin。你只需要一行bash命令export PATH=$PATH:/usr/locar/new/bin。这条命令的意思太清楚不过了，使PATH自增:/usr/locar/new/bin,既PATH=PATH+":/usr/locar/new/bin";通常的做法是把这行bash命令写到/root/.bashrc的末尾，然后当你重新登陆LINUX的时候（应该是linux启动时就会执行这个文件），新的默认路径就添加进去了。当然这里你直接用source /root/.bashrc执行这个文件重新登陆了。你可以用echo $PATH命令查看PATH的值。


# 关于删除自定义路径：
> 当某天你发现你新增的路径/usr/locar/new/bin已经没用了的话，你可以修改/root/.bashrc文件里面你新增的路径。或者你可以修改/etc/profile文件删除你不需要的路径.

一般来说，配置交叉编译工具链的时候需要指定编译工具的路径，此时就需要设置环境变量。例如我的mips-linux-gcc编译器在“/opt/au1200_rm/build_tools/bin”目录下，build_tools就是我的编译工具，则有如下三种方法来设置环境变量：
--------------------------------------------
临时环境变量(重启后消失)
-----------------------------------------------------
* 直接用export命令：
`#export PATH=$PATH:/opt/au1200_rm/build_tools/bin ` 

查看是否已经设好，可用命令export查看：
```
[root@localhost bin]# export
declare -x BASH_ENV="/root/.bashrc"
declare -x G_BROKEN_FILENAMES="1"
declare -x HISTSIZE="1000"
declare -x HOME="/root"
declare -x HOSTNAME="localhost.localdomain"
declare -x INPUTRC="/etc/inputrc"
declare -x LANG="zh_CN.GB18030"
declare -x LANGUAGE="zh_CN.GB18030:zh_CN.GB2312:zh_CN"
declare -x LESSOPEN="|/usr/bin/lesspipe.sh %s"
declare -x LOGNAME="root"
declare -x LS_COLORS="no=00:fi=00:di=01;34:ln=01;36:pi=40;33:so=01;35:bd=40;33;01:cd=40;33;01:or=01;05;37;41:mi=01;05;37;41:ex=01;32:*.cmd=01;32:*.exe=01;32:*.com=01;32:*.btm=01;32:*.bat=01;32:*.sh=01;32:*.csh=01;32:*.tar=01;31:*.tgz=01;31:*.arj=01;31:*.taz=01;31:*.lzh=01;31:*.zip=01;31:*.z=01;31:*.Z=01;31:*.gz=01;31:*.bz2=01;31:*.bz=01;31:*.tz=01;31:*.rpm=01;31:*.cpio=01;31:*.jpg=01;35:*.gif=01;35:*.bmp=01;35:*.xbm=01;35:*.xpm=01;35:*.png=01;35:*.tif=01;35:"
declare -x MAIL="/var/spool/mail/root"
declare -x OLDPWD="/opt/au1200_rm/build_tools"
declare -x PATH="/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/usr/X11R6/bin:/root/bin:/opt/au1200_rm/build_tools/bin"
declare -x PWD="/opt/au1200_rm/build_tools/bin"
declare -x SHELL="/bin/bash"
declare -x SHLVL="1"
declare -x SSH_ASKPASS="/usr/libexec/openssh/gnome-ssh-askpass"
declare -x SSH_AUTH_SOCK="/tmp/ssh-XX3LKWhz/agent.4242"
declare -x SSH_CLIENT="10.3.37.152 2236 22"
declare -x SSH_CONNECTION="10.3.37.152 2236 10.3.37.186 22"
declare -x SSH_TTY="/dev/pts/2"
declare -x TERM="linux"
declare -x USER="root"
declare -x USERNAME="root"

```
> 可以看到，环境变量已经设好，PATH里面已经有了我要加的编译器的路径。
里去操作了。

永久环境变量
--------------------------------------------------------
* 修改profile文件：
 所有用户(不安全)
 修 改`/etc/profile`（对所有用户都是有效的）
`#vi /etc/profile`
在里面加入:
`export PATH="$PATH:/opt/au1200_rm/build_tools/bin"`

* 修改.bashrc文件：
`# vi /~/.bashrc`
 (单独用户)
 修改~/.bashrc文件。 htt(74)p://www.icwin.net/bbs http://www.wantso.com （每个用户目录下都有，ls -all）
 ```
 cd ~
 vi .bashrc
 ```
在里面加入：
`export PATH="$PATH:/opt/au1200_rm/build_tools/bin"`

> 后两种方法一般需要重新注销系统才能生效，最后可以通过echo命令测试一下：
# echo $PATH
> 看看输出里面是不是已经有了/my_new_path这个路径了。

-----------------------------------------------------------------------------------------------------------------------

> 　“/bin”、“/sbin”、“/usr/bin”、“/usr/sbin”、“/usr/local/bin”等路径已经在系统环境变量中了，如果可执行文件在这几个标准位置，在终端命令行输入该软件可执行文件的文件名和参数(如果需要参数)，回车即可。

>　　如果不在标准位置，文件名前面需要加上完整的路径。不过每次都这样跑就太麻烦了，一个“一劳永逸”的办法是把这个路径加入环境变量。命令 “PATH=$PATH:路径”可以把这个路径加入环境变量，但是退出这个命令行就失效了。要想永久生效，需要把这行添加到环境变量文件里。有两个文件可选：“/etc/profile”和用户主目录下的“.bash_profile”，“/etc/profile”对系统里所有用户都有效，用户主目录下的“.bash_profile”只对这个用户有效。

>　　“PATH=$PATH:路径1:路径2:...:路径n”，意思是可执行文件的路径包括原先设定的路径，也包括从“路径1”到“路径n”的所有路径。当用户输入一个一串字符并按回车后，shell会依次在这些路径里找对应的可执行文件并交给系统核心执行。那个“$PATH”表示原先设定的路径仍然有效，注意不要漏掉。某些软件可能还有“PATH”以外类型的环境变量需要添加，但方法与此相同，并且也需要注意“$”。

>　　注意，与DOS/Window不同，UNIX类系统环境变量中路径名用冒号分隔，不是分号。另外，软件越装越多，环境变量越添越多，为了避免造成混乱，建议所有语句都添加在文件结尾，按软件的安装顺序添加。

>　　格式如下()：
```

　　# 软件名-版本号

　　PATH=$PATH:路径1:路径2:...:路径n

　　其他环境变量=$其他环境变量:...

```
>　　在“profile”和“.bash_profile”中，“#”是注释符号，写在这里除了视觉分隔外没有任何效果。

>　　设置完毕，注销并重新登录，设置就生效了。如果不注销，直接在shell里执行这些语句，也能生效，但是作用范围只限于执行了这些语句的shell。

>　　相关的环境变量生效后，就不必老跑到软件的可执行文件目录
