---
layout: post
title: "magento中调用js文件的几种方法"
tags:
- Magento
---
 
###一、全局调用方法：

通过该方法每个页面都会引用这个JS文件，除非是类似jQuery这样的系统文件，不然不推荐这种方法。

文件路径：

	/app/design/frontend/default/Your_Template/layout/page.xml

你会看到很多类似于addJS这样的XML代码，这是magento的优势之一，通过XML来配置文件很方便灵活。

如下：

	<action method="addJs"><script>varien/js.js</script></action>
	<action method="addJs"><script>varien/form.js</script></action>
	<action method="addJs"><script>varien/menu.js</script></action>
	<action method="addJs"><script>mage/translate.js</script></action>
	<action method="addJs"><script>mage/cookies.js</script></action>

###二、你也可以在phtml页面通过Magento自带的帮助函数来引用JS，例如：

	<?php echo $this->helper('core/js')->includeScript('varien/js.js') ?>

该方法主要用来在某些特定页面包含额外的js文件。而这些文件在其他页面中却不常使用。

###三、包含特定Theme包下的js文件：

再方便点，下面的方法很眼熟吧

	<script type="text/javascript" src="<?php echo $this->getSkinUrl('js/slider.js') ?>"></script>

它引用的是模板目录下js文件夹里面的js文件，我喜欢用这种方法。

###四、在对应的block类中调用JS

	protected function_prepareLayout(){
	$this->getLayout()->getBlock('head')->addJs('mage/adminhtml/sales.js');
	…..
	returnparent::_prepareLayout();
	}

这个方法我个人是很少用到的。

###五、直接将JavaScript代码写在head头部里：

打开

	app/design/frontend/default/Your_Template/template/page/html/head.phtml

JS代码写在
	
	<?php echo $this->helper('core/js')->getTranslatorScript() ?>
	
这行下面

此方法适合添加Google分析跟踪代码或者其它JS代码。