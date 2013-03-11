--- 
tags: 
- Dropbox
- Linux

layout: post
published: true
type: post
title: 用DropBox来同步备份linux数据

meta: 
  _edit_last: "1"
status: publish
---
Linux下安装

具体见：https://www.dropbox.com/install?os=lnx

32-bit:

	cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86" | tar xzf -
64-bit:

	cd ~ && wget -O - "https://www.dropbox.com/download?plat=lnx.x86_64" | tar xzf -

Next, run the Dropbox daemon from the newly created .dropbox-dist folder.

	~/.dropbox-dist/dropboxd

If you're running Dropbox on your server for the first time, you'll be asked to copy and paste a link in a working browser to create a new account or add your server to an existing account. Once you do, your Dropbox folder will be created in your home directory. Download this CLI script to control Dropbox from the command line. For easy access, put a symlink to the script anywhere in your PATH.

备份：

	cd ~/Dropbox
	ln -s /var/www web_backup

这就可以了,或者要备份/etc目录
