+++
title = 'Linux How To'
date = 2023-11-05T14:57:53+08:00
draft = false
tags = ["cheatsheet"]
+++

主要记录Linux下常用命令的CheatSheet
<!--more-->
# Linux 命令手册

#### 1.APT

* `apt update`:该命令会根据配置文件中的源更新本地的软件仓库数据库。对于每一个源，会有三种状态，在执行完毕之后，会有一个本次`update`的汇总信息，包括是否有可更新的软件。
  * 获取：连接到对应的服务器，但是没有需要更新的
  * 下载：连接到对应的服务器，并且数据库有变化
  * 忽略：表示无更新或者更新是无关紧要的

* `apt list --upgradable`:检查更新

* `apt list --installed`:显示已经安装的软件包

* `apt upgrade`:升级软件。系统会先做一个检查，然后会询问你是否需要升级软件。如果不指定对应软件，系统会升级所有的软件。

* `apt install package_name`:安装对应的软件，如果不清楚软件的名字不要紧，可以输入部分的名字

* `apt install -f：`自动修复依赖关系，在`dpkg-i`安装失败之后使用这个尤其有用

* `apt remove package_name&&apt autoremove`:前者删除某一个软件包，后者则使用自动删除他调用的依赖。

* `apt show package_name:`显示软件包的详细信息

* `apt-get dist-upgrade:`升级系统

  NB:与APT有关的文件有两个，一个是`/etc/apt/source.list`文件，这个文件记录了对应的源服务器地址。另外一个文件是`/var/lib/opt/lists`中的文件。更深入一点，事实上，我们每次执行`apt update`的时候，都是在服务器中下载对应的文件`Packages/Sources/Release`和本地的文件进行对比，如果不同则更新。这些本地的索引文件包含了对应文件的链接、依赖关系等。

#### 2. DPKG

* `dpkg -i package_name`:安装对应的Package.
* `dpkg -l|package_key_words：`列出所有的文件和当前的状态
* `dpkg -L package_name:`列出对应Package的安装位置
* `dpkg -r package_name:`删除对应的安装包，保留配置文件
* `dpkg -P package_name:`删除关于一个安装包的所有文件
* `dpkg -s file_name_Pattern:`显示一个包的相信信息

#### 3. Shell 光标

* `ctrl+a:`跳转到行首
* `ctrl+e:`跳转到行末尾
* `ctrl+u:`删除光标前的数据
* `ctrl+k:`删除光标后的数据
* `ctrl+w:`删除一个单词
* `ctrl+<-/->:`以单词为单位跳转
* `ctrl+y:`粘贴
* `alt+d:`向后删除

#### ４.GIT概述

* 版本控制：所谓版本就是开发不断迭代过程中一次打包和发布。在不考虑用户的前提下，开发的过程中为什么需要进行不断的打包和发布呢？最直观的原因就是我们的开发往往是一个一个模块地进行的，在一些时刻，即使系统没有被开发完成，但是某一个模块却可能是开发完整的。在这个时候，如果不对系统进行一次快照（可以认为是一次发布、备份）的话，在后续的开发过程中，可能需要不断地修改代码（包括已经写好的代码），可能系统陷入`bug`的泥潭。这个时候铁着头修改代码可能不如直接返工来的快。这就是版本控制的好处，一个版本就是系统的一个状态，一个milestone.
* 集中化的版本控制VS分布式的版本控制：所谓集中化的版本控制系统就是有一个服务器专门提供版本数据的存储。所有的客户端都来链接到这个服务器获取**最新的**文件或者提交更新。集中化的版本控制高度依赖于中心的服务器，如果服务器因为一些原因不能正常工作（例如断电、宕机、硬件损坏等），整个版本的更迭无法正常进行；分布式版本控制则不同，**每一次客户端的拷贝都是对代码仓库的一次完整镜像**。`Git`有如下的一些优势：工作的时候不需要联网。只要把代码进行一次`clone`之后，你的电脑就是一台服务器，你可以尽情地进行版本的提交。不同的人只需要互相把修改的内容推给对方即可；而且更加安全：没有中央服务器的概念，每个人都是一个完整的代码仓库和版本仓库。
* GIT的配置文件：
  * `/etc/gitconfig`：全局的系统配置文件，如果使用`--system`选项的时候，会从该文件读取配置
  * `~/.gitconfig`或者`~/.config/git/config`文件：针对当前用户的配置文件，如果使用`--global`会使用该配置文件
  * `./.git/config`:针对当前仓库的配置文件，每一个级别的配置文件都会覆盖上一个级别的配置文件

* GIT的用户信息：安装`GIT`之后的第一件事情就是配置`GIT`的用户信息，使用对应的选项保存在对应的配置文件中。

* `.gitignore:`被`.gitignore`所指定的文件，不会被纳入到版本控制中。这些文件通常是`JAVA`的`.class`文件，`IEDA`生成的`idea`目录或者`Eclipse`生成的`.setting`目录等等。`Github`上的一个很好的项目提供了很多常用的语言的`.gitignore`模板。

  []: https://github.com/github/gitignore	"c"

* 文件状态：
  * 已修改：`modified`.表示已经修改了文件，但是没有保存在数据库中。
  * 已暂存：`staged`.表示对一个已修改文件的当前版本做了标记，使之包含在下一次提交的快照中。
  * 已提交：表示已经将数据保存在本地的数据库中。

* `GIT`常用命令总览：

  ![img](https://mmbiz.qpic.cn/mmbiz/9Eibnmwqk0Ajsad34njicm2Z2G1hYbRFV0QwQOnyibLC5dTe3qLpYBicsibY9pyRzwKdPicHBYcJ3WXWJ3ia8LicbTJB5Q/640?wx_fmt=other&tp=webp&wxfrom=5&wx_lazy=1&wx_co=1)

#### 5. GIT命令详解

* 创建工作区

  ```shell
  #via ssh
  git clone ssh://user@domain.com/repo.git
  #via http
  git clone http://domain.com/user/repo.git
  #create a local working directory
  git init
  ```

* 将文件从已修改添加到暂存区

  ```shell
  #Add the specified file to staged list.(ready for the commit)
  git add file_name
  #Add all the files to staged list.
  git add .
  ```

* 将文件提交到本地的数据库

  ```shell
  #commit the files in the staged list.
  git commit
  #commit the files in the staged list with a message
  git commit -m
  #commit the files modified
  git commit -a
  ```

* 使用草稿功能

  ```shell
  #You can not use the branch function if you have #files staged or modified.In this case or other cases,you can save the modification into stash
  #For the detailed usage,please see the following examples

  #save the current modification into stash and clear the current master
  git stash
  #see the stash list
  git stash list
  #delete a stash
  git stash drop stash_num
  #apply a stash
  git stash apply stash_num
  ```

* 回退

  ```shell
  #HEAD is a environmental variable which records the most lately version.
  #--hard option is used to drop the modifition,else all the modifitions are saved

  #remove all the staged info and modification(use the hard option to remove all the modification,if not specified,will save the modifition)
  git reset --hard HEAD
  #reset to a specified versin (use hard option to remove all the modified infomation)
  git reset [--hard] <commit-info>

  #reset the specified file to the most lately version
  git checkout HEAD filename
  ```

* 查看日志

  ```shell
  #see all the commits
  git log
  #specify the author
  git log --author='march1917'
  #specify the file
  git log -p README
  ```

* 在文件中进行搜索

  ```shell
  git grep grep_pattern
  ```

* 分支：

  ```shell
  #show all the branches
  #use -r option to list the remote branches only
  git [-r] branch

  #to make a new branch based on the current branch
    git branch branch_name

    #to checkout a branch.use -b option if the target branch is not exist.it will create a new branch
    git checkout [-b] branch_name

    #to remove a branch (you can excute this command only when your different branch are merged)
    git branch -d branch_name

    #Force to delete a branch even if the modification is not merged.
    git branch -D branch_name

    #to merge a branch to current branch(curupts are not accepted)
    git merge target-branch
  ```


#### 6.EXPECT

* expect:expect是一种类似`BASH`的`SHELL`脚本语言，我们写好的脚本交给他执行即可。expect在处理自动化输入输出交互方面优势尤为突出

* expect的四个基本关键字：

  * `spawn:`启动一个命令
  * `expect:`从程序读取一个字符串，支持正则表达式
  * `send:`向程序发送一个字符串
  * `interact:`允许真人用户参与交互



* expect中的变量*：
  * `$expect_out(buffer)`:程序的实际输入
  * `$expect_out(0,buffer):`程序语气的输入

* 模式－动作：

  ```bash
  #!/usr/bin/expect
  #可以写的很简单，用字符串分隔开即可
  expect "hi"
  send "hi"
  #也可以带有分支
  expect {
  "hi" {send "you hi too"}
  "hello" {send "hello too"}
  "bye" {send "do not wanna say goodbye to you"}
  }
  ```

* 和进程对话——关键字`spawn`:如果不使用这个关键字，那么就只能对标准输入进行预测然后进行输出。但是`spawn`关键字使得我们可以和进程对话。

* 让用户参与其中：在一些特殊的场合中，我们需要人来参与其中，这个时候就可以使用`interact`关键字

* 注意事项：

  * 不要忘记使用`\n`
  * 严格按照原来的语法规则使用，例如数据库操作中的`;`
  * 使用`interact`关键字可以很好地实现半自动化（大部分场合我们并不需要全自动化，只是省去一些繁琐的步骤而已）



#### 7. 使用静态库文件

* 静态库文件和动态库文件：静态库文件和动态库文件都具有共享性，即一次编译之后可以被其他程序调用而不必重复编写。但是机制上又存在一些不同。静态库文件在编译的时候将静态库文件中的文件拿来整合到可执行文件之中。而动态库文件则不同动态库文件在编译的时候只会保留一个对库文件的链接，在加载或者运行的时候才会将代码加载过来。

* 静态库文件和动态库文件的标识：在`Linux`中静态库文件使用`.a`结尾，动态库文件使用`.so`结尾。在`Windows`中，静态库文件使用`.lib`结尾，动态库文件使用`.dll`结尾。

* 使用静态库文件：静态库文件必须和静态使用（即在编译的时候必须将库文件整合进来）。

  ```shell
  g++ -c myadd.cpp #generate the obj file
  ar rcs mylib.a myadd.o #generate the lib file

  #The following commands show how to use the static lib
  g++ -c main.cpp
  g++ -static main main.o myadd.a

  #You can use like -lm option to specify the extra lib
  #you want to use.

  ```

  NB:静态库文件的顺序准则——库文件放后面；库文件之间被调用的放后面

#### 8.使用动态库文件

* 动态链接：共享库文件是一种特殊的可重定位目标文件，它可以在可执行文件加载或者运行的时候被动态地装入内存并自动链接。动态链接改善了静态链接占用磁盘空间的问题，而且更新不便。

* 使用动态库文件：

  ```shell
  #The follwing code show how to generate the .so file
  g++ -shared -fPIC myadd.so myadd.cpp

  #The follwing code show how to use the .so file
  g++ -o main main.c ./myadd.so
  ```

#### 9. Makefile

* Make: make是一个编译指令，可以用来简化编译相关的操作。

* make的基本语法：

  ```makefile
  #The follwing command show the basic grammar of make
  target:obj1.o obj2.o obj3.o
  	gcc option obj1.o obj2.o obj3.o
  #if there is only one target,you can use make to run
  #the target.But if there is other target,you have to
  #specify the target name.

  #The following command show the use of variables in makefile
  LIBS = -lm
  OBJS = obj1.o obj2.o obj3.o
  main:$(OBJS)
  	g++ $(LIBS) main OBJS

  #Actually,if one target relys on another target.you can put the target name on the right of comma.In this case,it will execute the corresponding command if  the target does not exist

  #use the function to get all the files path
  LIBS=$(wildcard,include/*.so)
  ```


#### 10. VIM

* 常用快捷键

  ```shell
  #Two comparision i-a I-A
  i:从当前字符开始插入
  I:从当前行的第一个非空格字符开始插入
  a:从当前字符的下一个字符开始插入
  A:从当前行的最后一个字符开始插入
  #The following instructions will make new lines
  o:从当前的下一行开始插入新的一行
  O：从当前行的上一行开始新的一行

  #delete a word
  de:删除到本单词的末尾
  db:删除到本单词的开头
  dE:效果同de，但是忽略标点
  dB:效果同db,但是忽略标点

  #move the cursor
  xG:跳转到某一行
  G:到末尾
  h/l/j/k:光标向左、向右、向上、向下移动
  0/^/$:到非空白文本最左边/到行首/到行尾
  gg：到第一行
  ```



#### 11.Grep && FP

* Grep

  ```shell
  #The basic use of grep.It will get from the standard input.
  grep string
  #Alternatively,we can set the --color=auto option to make it readable.
  grep string --color=auto
  #use -n option to show the line number
  grep -n string file_name
  #use -v option to invert the match.only show the not-matching lines.
  grep -v string file_name
  #use -i option to ignore the case distinctions.
  grep -vi string file_name
  #use [] to choose different character in a string,remeber [] will transfer to a single character
  ```



* formal expresion

  ```shell
  grep t[ae]st file_name
  #we can use ^ to filter some cases,for example the following will grep strings including 'oo' but will 'goo' will be excluded.
  grep [^g]oo file_name
  #use line init symbol ^,eg:the following command will filter the lines with 'the' beiginning
  grep ^the file_name
  #use . which denotes a signle char,\d denotes a digital \w denotes a digit or a english character,\s denotes a blank space or a tab or a enter.
  grep g..d file_name
  #use * which denotes any times repetition of last char
  grep goo*d file_name
  #use {} to specify the times of repitition,the following command will filter the lines goo gooo...
  grep go\{2,\}
  ```

* extend expression

  ```shell
  #use ? which denotes zero or one times of repetition.o and oo are accepted.
  egrep oo? filename
  #use + which denotes 1 or more times of repetition.o and oo and ooo... are acceptted.
  egrep o+ filename
  #use | to handle different cases.like and dislike will all be chosen.
  egrep like|dislike
  #use () which will first be transfered.glad and good will be accepted.+and * ? will work on () too.
  egrep g(la|oo)d

  ```

#### 12 SED
* general syntax:`sed -e '..' -e '...' source_file'
* additional options
  * -f: read the script from the file
  * -n: do not print anything unless the p command explictly is used
  * -i: by default, sed will not change the source file, -i enables it.
  * -r: use extend regular expression.
* general syntax:`[ADDR1]ACTION[OPTION1] or [ADDR]{ACTION_1[OPTION1];ACTION_2[OPTION2]`
* workflow of the sed script:
  * 1:Read a single line into the pattern buffer
  * 2:Apply all the commands to the pattern buffer
  * 3:Print(or not which depends on the p and n option) the pattern buffer and clear it
* Simply specify the line number: `number`
* Specify the line range:`2-5`
* Sxecify the line every x lines:`2~x`
* Pattern: `/RE/`
* Offset: `/Re/,+5 p/
* Negation: `2,5!` selct the first line and lines after 5.
* s:substitute,like `s/RE/replacement/[FLAGS]`.
  * you can also use any character as the delimeters
  * some frequently used flags:
    ```shell
    g:global
    number:ignore the match before the number th occurence and replace from the number th on
    p:if the substitution is made, print the new pattern space
    w:if the substitution is made,write out the specified file.the /dev/stderr and /dev/stdout are supported
    i:regular math case-insensitive
    m:allow multiple lines match
    ```
  * back reference: it is possible that use the back reference in your replacement part.`\1` means the first regular expression math. At most 10 references are supported.In particular, the & means the whole match.Well, if you want to use the back reference, you need to wrap the regular expression with "()".
* q:quit, you can also use Q which is used to stop the process.The difference between the q and Q is that q print the current line and quit while Q quits without printing anything.
* d:delete the pattern space,and also begin the next cycle immediately.
* p:print explictly
* n:replace the pattern buffer with next line.If `-n` is specified, do not print the former pattern buffer,else print the buffer.
* y:y is the command to transfer from the SRC set to the DST set which is like tr.
* i:insert before the current line
* a:append next to the current line
* c:change the current line
* l:l print the text in a unambigous way. like `aa$`
* =:print the line number
* z:zero, simply empty the pattern space
* e:execute a external unix command.
* h:copy the content of the pattern buffer to the hold buffer.
* H:append the pattern buffer to the hold buffer.
* g:copy the content of the hold buffer to the pattern buffer.
* G:append the hold buffer to the pattern buffer.
* x:exchange the hold buffer with the pattern buffer.
* D:delete a line from the pattern space until the first newline and restart the cycle.
* N:append a new line from the input file to the pattern space.
* P:print the line from the pattern buffer until the first new line.
* I:print data in a unambigous way.
#### 13 GDB
* To use GDB: gdb is most effective when it is debugging a program that has debugging symbols linked to it.With g++,this is accomplished with -g command option.For even more information, you can use -ggdb.
* To load a program:use gdb program_file
Trick:if you use makefile and find there are no sysmbols generated, please check if you add -g option to the final generation or at the complile(-c) proceed.ALL THE SYSBOLS ARE GENERATED AT THE COMPILE STAGE,NOT THE LINK STAGE!!!
```gdb
#begin to run until a breakpoint
r

#continue to run until a break point
c

#add breakpoints at the specific line in test.c
b test.c:10

#add the breakpoint at the specfic function
b add

#add the condition for the breakpoint
condition 1(breakpoint number) var == 1

#add a breakpoint at the current line
b

#delete a breakpoint
d number

#show all the break points
info break

#run the current function
f

#step N lines
s N

#add a watch point
watch a==2

#show all the watch points
info watch

#change the variable value
set x=1

#display the value of x
display x

#undisplay
undisplay x

#show the stack
bt

#move up the stack
up

#move down
down

#show the value of an address
x addr

#print the value
p x

#Some tips on debugging
# * Found the wrong line:if possible.An effective way is to use gdb to prceed line by line.
# * Debug as early as quickly
# * Debug elegantly:we understand that debugging sometimes is time-assuming and annoying.But leave your code clean after debug.(Do not use printf too much,it will mess everthing up)
```
 #### 14 MARKDOWN
* 单独添加链接：`[link name](link-url)`
* 引用：`[link name][link variable] [link-variable]:link-url`
* 添加图片：`![image-name][image-url]`
* 添加图片引用：`![link name][link-variable] [link-variable]:link-url`
* Block Reference
>some thing to reference
>
>blank line must also begin with >
* 为一个bullet list添加一段话：先输入一个空行，然后空出一个字符，开始写。
* 段落换行：使用两个空格
* 下划线：`<u>text</u>`
* 删除线：`~~text to delete~~`

#### 15 CONFIGURE THE SSH KEY
* 使用`ssh-keygen -t rsa`生成一个新的密码在用户目录下`~/.ssh/`下面
* 将公钥粘贴在`github`安全的密钥部分
* 以后使用的项目地址使用`git+ssh://git@github.com/username/repositoryname`

#### 16 使用cron
* 直接使用`crontab`命令即可访问编辑`crontab`服务。当见的参数如下图所示：
```shell
    -e 编辑当前用户的crontab
    -l 显示当前用户的crontab
    -u 编辑root用户的crontab
    -r 删除当前用户的crontab
```
* `crontab`的配置文件都存在于`/var/spool/cron/crontabs/user-name`
* `Ubuntu`用户默认的日志文件于`/var/log/syslog`,可以将`crontab`的配置文件单独弄出来使用下面的办法：
>modify rsyslog config: open /etc/rsyslog.d/50-default.conf,remove # before cron.*
>restart rsyslog service: sudo service rsyslog restart
>restart cron service: service cron restart
>now you can check cron log from file /var/log/cron.log

#### 17 Python中的路径
* python中的路径有很多：
    * 文件的路径:`__file__`变量保存了文件的路径，具体是绝对路径还是相对路径取决于输入——即如果输入对该文件使用的是绝对路径则变量中保存的就也是绝对路径，反之亦然。可以使用`os.path.abspath(__file__)`得到文件的绝对路径。
    * 文件所在目录的路径：python提供了函数`os.path.split(abs_path)`可以将文件的**绝对路径**拆分为目录路径和文件名。但是一种更为方便的做法是使用`sys.path[0]`来获取文件所在的目录。
    * Python搜索模块的路径:`sys.path`存储模块的搜索目录，第一项是当前文件的目录。
    * 工作的路径:`getcwd`可以获取当前的工作目录，需要注意当前的工作目录和文件所在的目录没有必然关系。Python中打开文件搜索的是工作目录而非当前文件所在目录。可以使用`os.chcwd`函数来调整当前的工作目录。

#### 18. Tmux

##### Tmux
Tmux提供终端复用(terminal multiplexer)的能力。
![[Pasted image 20231208154016.png]]
具体来说tmux为用户提供了两项能力：
1. 在同一个终端连接内提供有多个Pane和Tab。所谓的pane，你可以认为是同一个屏幕内划分为多个区域，tab则和现代浏览器的标签一样，在tmux中也叫window。
2. 创建多个session的能力，一个session可以保存也可以退出，不会因为SSH连接的断开而挂掉。一个任务可以被看作一个context，可以在不同的context中间切换。

>为什么不直接采用多个窗口呢，毕竟像一些现代的终端其实也都提供了分屏的功能。因为在tmux中，每个终端的任务是以文件的方式存储的，不会因为连接断开就直接挂掉。在一些比较严苛的环境下，tmux也可以正常使用，这一点可以类比VIM。


##### 创建session

* 直接创建一个session: `tmux`。此时创建一个按序号命名的session，并将此session调度到台前。
* 创建一个新的带名字的session: `tmux new -s session_name`。

##### session的调度

* detach: 创建一个session后，默认进入当前session(调度到前台)。如果想要退出当前的session，使用`tmux detach`. 即可从当前的session**暂时**退出，即该session被放到了后台。对应的快捷键：ctrl-b d。
* ls: 退出当前的session后，使用`tmux ls`即可查看当前的所有的session.
* attach: 如果想要进入某个session，使用`tmux attach -t target-session 。
* next and previous: 如果在一个session,使用`ctrl b + (`和`ctrl b + )`切换到前一个和下一个session. 如果想看所有的session，使用`ctrl + b + s`
##### 分屏
* 左右拆分：**在一个tmux session内部**，ctrl-b + %。
* 上下拆分：**在一个tmux session内部**，ctrl-b + “。
* 在不同的屏幕内跳转：**在一个tmux session内部**，ctrl-b + \<arrow-key\>。
* 退出一个pane: 直接执行exit/ctrl-d即可。
* 调整当前的pane大小：ctrl/b + crtl + arrow

##### Window
tmux支持在一个session内部有多个窗口，这个功能类似于浏览器的标签。个人感觉window不是很实用，其实到session这个粒度其实已经可以了。不过我看了一下也很简单，就也记录一下。
* 创建window: **在一个tmux session内部**，ctrl-b + c(reate)。
* 下一个window: **在一个tmux session内部**，ctrl-b + n(ext)。
* 上一个window: **在一个tmux session内部**，ctrl-b + p(revious)。
* 查看所有的window: **在一个tmux session内部**，ctrl-b + w(indow)。


>参考链接：
>[Tmux — An awesome terminal multiplexer](https://blog.devgenius.io/tmux-an-awesome-terminal-multiplexer-62609c6916bb)
>[Tmux Cheatsheet](https://tmuxcheatsheet.com)



