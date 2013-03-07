--- 
tags: 
- Magento
layout: post
published: true
type: post
title: 解决“Magento Service Temporarily Unavailable”.md
meta: 
  _edit_last: "1"
status: publish
---
Service Temporarily Unavailable是Magento常见的一个错误之一，通常会在Magento版本更新或者插件的安装及升级过程中出现该错误提示。需要注意的是，该提示在Magento及其插件升级的过程中是肯定会显示在前台页面的，虽然时间很短。之所以说它是一个错误提示，主要是在版本升级错误或者插件安装失败的情况下。

<!--more-->

![Magento错误提示][1]

Service Temporarily Unavailable字面意思是此服务暂时无法使用，如果说你对Magento的各项操作已经完成的情况下，仍然出现该提示，那么下面的方法可以帮助你解决问题。首先，打开安装的Magento的根目录，应该能发现一个maintenance.flag文件，将该文件删除。接着打开根目录下的var目录，删除其中的cache缓存文件夹。完成这两项操作之后，刷新前台就能够正常显示了。 最后，你需要之后导致这项错误的原因，如果是因为插件安装的问题，建议你到插件安装界面卸载该插件，或者在安装目录中找到那些文件，手动安装，保证Magento的正常运行。

 [1]: http://www.libokai.com/wp-content/uploads/2013/02/b01870dea3cc7cd9b539c96d3901213fb90e91ac-300x189.png