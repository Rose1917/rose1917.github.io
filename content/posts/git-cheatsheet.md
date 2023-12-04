+++
title = 'Git Cheatsheet'
date = 2023-12-04T10:07:05+08:00
draft = false
tags = ["cheatsheet"]
+++

git cheatsheet
<!--more-->

#### git clone
* ``git clone --depth=1`` 执行了一个浅克隆操作。--depth=1 参数告诉 Git 只克隆最近的一次提交及其相关的文件、分支和标签。
>浅克隆是指只克隆 Git 存储库的最新版本历史记录，而不克隆完整的历史记录。
>需要注意的是，浅克隆的一个限制是无法执行某些操作，如查看或检出过去的提交，因为它们不在克隆的范围内。如果你需要完整的历史记录，可以使用 git fetch --unshallow 命令将浅克隆转换为完整克隆。

#### git submodule
在 Git 中，submodule 是一种机制，允许你将一个 Git 存储库嵌套在另一个 Git 存储库中。这对于管理项目依赖关系或使用外部代码库非常有用。
* 添加子模块: 要将一个子模块添加到主存储库中，可以使用 ``git submodule add`` 命令.
```s要将一个子模块添加到主存储库中，可以使用 git submodule add 命令：hel
git submodule add <repository_url> <path>
`````````
* 克隆：在克隆主存储库之后，子模块目录是空的。你需要初始化子模块并获取其内容。可以使用以下命令来完成初始化.
``````shell
git submodule init
git submodule update
``````
> 第一个命令 git submodule init 会初始化子模块，将其连接到正确的提交。第二个命令 git submodule update 会获取子模块的内容并检出合适的版本。

* 更新：如果子模块的远程存储库有新的提交，你可以使用以下命令更新子模块：
```ssh
git submodule update --remote 
```

