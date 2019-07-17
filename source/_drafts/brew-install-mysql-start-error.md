---
title: brew 安装 MySQL 遇到的错误
date: 2015-10-14 21:13:10
---

```
brew install mysql
```

出现如下错误：

```
mysql -uroot 进入mysql
```


```
ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)
```

```
mysql.server start 启动mysql.server
```


```
ERROR! The server quit without updating PID file (/usr/local/var/mysql/user.local.pid).
```

解决办法：

```
brew postinstall mysql
```

```
mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp
```

```
ln -sfv /usr/local/opt/mysql/homebrew.mxcl.mysql.plist ~/Library/LaunchAgents
```

```
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.mysql.plist
```

```sudo chown -R [user]:admin /usr/local/var/mysql ```
