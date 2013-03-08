--- 
tags: 
- ubuntu
- mysql
layout: post
published: true
type: post
title: ubuntu server安装mysql时错误汇总

meta: 
  _edit_last: "1"
status: publish
---
在Mac下新装的ubuntu server虚拟机，安装源码mysql时遇到了各种问题，汇总如下：

<!--more-->

1

`Curses library not found.  Please install appropriate package,
remove CMakeCache.txt and rerun cmake.On Debian/Ubuntu, package name is libncurses5-dev, on Redhat and derivates it is ncurses-devel.`

按照错误提示，我的是utuntu，需要安装libncurses5-dev，

只需

`sudo apt-get install libncurses5-dev`

并且删除 CMakeCache.txt 重新cmake即可

2

`Warning: Bison executable not found in PATH`

需要

`apt-get install bison`

3

`CMake Error: CMAKE_CXX_COMPILER not set, after EnableLanguage
CMake Error: Internal CMake error, TryCompile configure of cmake failed
-- Performing Test HAVE_PEERCRED - Failed
-- Googlemock was not found. gtest-based unit tests will be disabled. You can run cmake . -DENABLE_DOWNLOADS=1 to automatically download and build required components from source.`

cmake时需要加上

`-DENABLE_DOWNLOADS=1`