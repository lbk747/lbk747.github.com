--- 
tags: 
- Magento
layout: post
published: true
type: post
title: 解决“Could not determine temp directory, please specify a cache_dir manuall”
meta: 
  _edit_last: "1"
status: publish
---
错误提示如下：

    Could not determine temp directory, please specify a cache_dir manually
    

<!--more-->

解决办法：

1.用记事本或其他文本编辑器打开

    magento/lib/Zend/Cache/Backend/File.php；
    

2.修改以下代码：

    protected $_options = array(
        'cache_dir' => null,
    
    修改后如下
    protected $_options = array(
        'cache_dir' => 'tmp/',
    

3.在magento目录下新建文件夹tmp，设置该文件夹访问权限为可写

通过以上三步即可解决此问题。