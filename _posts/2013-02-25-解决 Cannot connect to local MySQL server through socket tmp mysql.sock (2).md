--- 
tags: 
- Linux
- Mysql
layout: post
published: true
type: post
title: 解决“Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)”

meta: 
  _edit_last: "1"
status: publish
---
找不到mysql socket的问题，碰到过好多次

首先是mysqld启动不了，

我通过vim /etc/my.cnf，修改了[mysqld]选项下面的socket的值

`socket=/var/lib/mysql/mysql.sock`

ok，mysqld可以启动了

接下来，是mysql启动不了，同样，vim /etc/my.cnf,添加了如下脚本：

<!--more-->

`[mysql]
socket=/var/lib/mysql/mysql.sock`

然后，mysqladmin启动不了，还是一样，在[mysqladmin]下面socket值设置为同样的路径

ok,可以启动了

最后，用php连接的时候，又出现这个问题了

`Can't connect to local MySQL server through socket '/tmp/mysql.sock' (2)`

我首先想到的是，在/etc/php.ini修改mysql.default\_socket的值，在这个文件中，关于mysql.default\_socket的值的说明是这样的，

`; Default socket name for local MySQL connects.  If empty, uses the built-in MySQL defaults.`

这个值一开始是空的，也就是说，如果我们不主动去修改的话，php将会使用内建在mysql中的默认值

于是，我修改了这个值，设置为：

`mysql.default_socket=/var/lib/mysql/mysql.sock`

然后我重新启动apache，结果无效；reboot系统，结果无效

我火大了，php就非得去连接/tmp/mysql.sock，可是我的系统里面就是没有这个路径下的这个文件，那我就给你链接一个，于是我做了下面的操作，

`ln -s /var/lib/mysql/mysql.sock /tmp/mysql.sock`

重新打开我的php页面，ok，这下能连接到数据库了。

就这样，我把这个问题解决了，可是我还是有点迷糊，为什么一定要去找/tmp/mysql.sock这个文件，是不是一开始我就给它ln一个链接就可以解决？这个mysql.sock到底是用来做什么的？于是我就产生了看看这个文件内容的想法,

`cat /var/lib/mysql/mysql.sock`

提示我，cat: /var/lib/mysql/mysql.sock: 没有那个设备或地址

`less /var/lib/mysql/mysql.sock
/var/lib/mysql/mysql.sock is not a regular file (use -f to see it)`

我强行查看！

`less -f /var/lib/mysql/mysql.sock
/var/lib/mysql/mysql.sock: 没有那个设备或地址`

`vim /var/lib/mysql/mysql.sock`

提示权限不足，我是root用户耶，还提示权限不足，奇怪了

`ll /var/lib/mysql/mysql.sock`

看到的属性是：

`srwxrwxrwx 1 mysql mysql 0 11-21 14:39 /var/lib/mysql/mysql.sock`

这 个属性引起了我的注意，档案类型标志是s,还真没去了解过这样的类型，到鸟哥的私房菜去找了一下，原来，这个是资料接口档，用我们大陆说的习惯应该是套接 字文件(sockets)，这种文件一般用在网络上的资料套接，mysqld守护进程生成了这个文件，其他与mysql相关的程序想使用mysql，估计 就是通过这个文件了。

这种特殊文件即使是最高权限的root用户，也是不能查看不能编辑的，有点像档案标志是p的管道文件。

摘自：http://www.blogjava.net/asenyifei/articles/82575.html