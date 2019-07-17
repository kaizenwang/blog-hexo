---
title: 日常使用 git 命令
date: 2015-09-14 13:12:30
---

Git 命令
========

初始化`git repository`,在repository目录下运行

```
git init
```

#### git add

添加文件到暂存区, `.`为添加当前目录下全部文件

```
git add .
```

添加本地有改动的所有文件到暂存区`包括删除和修改`

```
git add -u
```

#### git commit

提交暂存区中内容提交到分支`""`中添加对本次操作的描述

```
git commit -m ""
```

#### git submodule

为当前repository 添加submodule

`仓库路径`submodule 的远程仓库地址

`文件路径`submodule 存放的地址

完成后在当前工程路径生成名为.gitmodules的文件

```
git submodule add 仓库地址 文件路径
```

下载submodule的内容,clone 下工程时不会下载submodule的内容,需要执行以下命令

```
git submodule update --init --recursive
```

删除submodule,首先要在`.gitmodules`文件中删除相应配置信息。

然后执行`git rm --cached`命令将子模块所在的文件从git中删除。

---

`暂存区:stage`
