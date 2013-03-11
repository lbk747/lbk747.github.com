--- 
tags: 
- Windows 8

layout: post
published: true
type: post
title:   Windows8中视频播放器框架player Framework的简单使用

meta: 
  _edit_last: "1"
status: publish
---

微软媒体平台的Player Framework是一个开源且强大的视频播放器框架，它是完全开源的，我们能够进行进一步开发和完善，支持Silverlight, HTML5, Windows Phone, Xbox, and Windows 8。

他们最近发布了版本为1.1的PXlayer Framework for Windows 8 and Windows Phone 8，下面来简单介绍下在windows 8中，这个强大框架的使用。

<!--more-->

1 下载[Player Framework for Windows 8 and WP8][1]扩展，并且安装。 ![QQ截图20130222095721.png][2]

2 创建一个基于C#的空白应用 ![v1.png][3]

3 添加Microsoft Player Framework的引用 ![v2.png][4] ![v3.png][5]

4 在xaml中添加PlayerFramework的命名空间

`xmlns:mmppf="using:Microsoft.PlayerFramework"`

5 添加MediaPalyer控件，并指定Source

`<Grid Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
    <mmppf:MediaPlayer Source="http://smf.blob.core.windows.net/samples/videos/bigbuck.mp4"/>
</Grid>`

现在就可以开始运行了 ![v4.png][6]

# 添加流媒体支持

--- 
tags: 
- !binary |
  5pyq5YiG57G7

layout: post
published: true
type: post
title: !binary |
  dWJ1bnR1IHNlcnZlcuWuieijhW15c3Fs5pe26ZSZ6K+v5rGH5oC7

meta: 
  _edit_last: "1"
status: publish
---

1 安装[Microsoft Smooth Streaming Client SDK for Windows 8 ][7](单独下载).

2 添加引用：Microsoft Player Framework，Microsoft Smooth Streaming Client SDK for Windows 8 ，Microsoft Visual C++ Runtime Package ，Microsoft Player Framework Adaptive Streaming Plugin ![v5.png][8]

3 在xaml中添加命名空间

`xmlns:mmppf="using:Microsoft.PlayerFramework" xmlns:adaptive="using:Microsoft.PlayerFramework.Adaptive"`

4 添加控件，并指定流媒体

`<mmppf:MediaPlayer Source="http://mediadl.microsoft.com/mediadl/iisnet/smoothmedia/Experience/BigBuckBunny_720p.ism/Manifest">
    <mmppf:MediaPlayer.Plugins>
        <adaptive:AdaptivePlugin />
    </mmppf:MediaPlayer.Plugins>
</mmppf:MediaPlayer>`

5 再被指管理器中指定应用平台为 x86，x64或者ARM，这是由于IIS流媒体客户端写在非托管的代码中，AnyCPU是不会工作的，所以需要为每一个平台分别编译

![v6.png][9]

现在就可以开始运行了 ![v7.png][10]

更多用法可以参考：http://playerframework.codeplex.com/

 [1]: http://playerframework.codeplex.com/releases
 [2]: http://a1.eoe.cn/www/home/201302/22/5396/5126d0925327f.png "QQ截图20130222095721.png"
 [3]: http://a1.eoe.cn/www/home/201302/22/e310/5126d12fe7897.png "v1.png"
 [4]: http://a1.eoe.cn/www/home/201302/22/072a/5126d444780cc.png "v2.png"
 [5]: http://a1.eoe.cn/www/home/201302/22/2eec/5126d476039d6.png "v3.png"
 [6]: http://a1.eoe.cn/www/home/201302/22/953e/5126d6ab9360b.png "v4.png"
 [7]: http://visualstudiogallery.msdn.microsoft.com/04423d13-3b3e-4741-a01c-1ae29e84fea6
 [8]: http://a1.eoe.cn/www/home/201302/22/f219/5126d9965f902.png "v5.png"
 [9]: http://a1.eoe.cn/www/home/201302/22/0c34/5126e0740e6a7.png "v6.png"
 [10]: http://a1.eoe.cn/www/home/201302/22/07d5/5126e12cdd776.png "v7.png"