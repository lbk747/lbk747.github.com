---
layout: post
title: CentOS安装memcache
tags:
- CentOS
- memcache

---

###首先导入第三方软件仓库RPMForge 

**32位**

	wget http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.i686.rpm
	
**64位**

	wget http://pkgs.repoforge.org/rpmforge-release/rpmforge-release-0.5.2-2.el6.rf.x86_64.rpm

**导入**

	rpm -ivh rpmforge-release-*.rpm

###查找相关软件包

	yum search memcache
	
###安装

	yum -y install –enablerepo=rpmforge memcached php-pecl-memcache
	
###验证一下安装结果

	memcached -h

	php -m|grep memcache

###设置开机启动

	chkconfig memcached on
	
###启动memcached

	service memcached start
