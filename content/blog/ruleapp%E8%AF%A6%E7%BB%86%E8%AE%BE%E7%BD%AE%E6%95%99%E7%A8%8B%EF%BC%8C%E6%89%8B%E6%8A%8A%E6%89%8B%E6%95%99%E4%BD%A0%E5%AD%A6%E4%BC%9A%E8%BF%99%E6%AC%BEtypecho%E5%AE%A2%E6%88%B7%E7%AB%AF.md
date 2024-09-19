---
title: RuleAPP详细设置教程，手把手教你学会这款Typecho客户端
date: 2024-09-19T13:01:49.786Z
---


[www.ruletree.club](https://www.ruletree.club/archives/2955/)RINGOLv.1 说道：

本教程主要是讲解RuleAPP的详细配置，包括数据的调用，第三方登录和在线支付的配置，以及如何对RuleAPP进行二次开发。在这篇教程中，除了基本的配置外，还会讲解目录的结构，开发的框架等信息，帮助各位更好的使用RuleAPP建设自己的客户端应用。到目前为止，正式版也已经即将推出，所以希望这篇教程能够帮助所有的用户掌握RuleAPP。

> RuleAPP是一款基于uniapp技术，ColorUI框架开发的Typecho客户端应用，目前已经兼容安卓苹果APP，H5网页，和微信QQ小程序。

下载地址：[点击进入](https://www.ruletree.club/go/aHR0cHM6Ly9leHQuZGNsb3VkLm5ldC5jbi9wbHVnaW4|aWQ9NjkwOQ==)-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "0.jpg")

0.jpg

首先要明确一点，RuleAPP是完全开源的，所有的地方都可以随意的修改删除或者增加新功能满足自己的需求。不过在开始自己修改之前，需要明白很多基本的配置。话不多说，开始讲解基本的配置教程。![](https://image.cubox.pro/article/2022040909060542881/13170.jpg)

## 全局配置部分

RuleAPP需要进行修改的配置文件主要有三个，`其中两个是uniapp自带的，分别是manifest.json和pages.json`，还有一个则是RuleAPP本身的全局配置文件/utils/api.js。

## 不过在这之前，先说下目录结构。

根据下图来看源码目录的所有信息。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "3.png")

3.png

## 然后，从/utils/api.js开始

RuleAPP的轮播图，推荐文章，和工具页面的软件工具，都是基于typecho标签的文章调用，并且在/utils/api.js中进行定义。而这个文件定义了整个APP的所有配置和接口的定义，打开后可以看到如下的页面。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "1.png")

1.png

### 1.先从开头的四个字段开始，它们分别如下：

    
       
       
        
        var API_URL = 'https://api.ruletree.club/';   //API地址
    
        
        var WEB_URL = 'https://www.ruletree.club/';   //Typecho网站地址
    
        
        var GroupUrl = 'https://jq.qq.com/?_wv=1027&k=XX5SFavQ';   //群聊地址
    
        
        var GithubUrl = 'https://github.com/buxia97/RuleApp';   //github地址
    
        
        
    
       
       

除了前两个比较重要外，剩下的两个都是可以自行去除或者DIY。比如，群聊地址的调用对应如下这里。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "2.png")

2.png

而github地址只有一个页面调用。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "4.png")

2.png

想必这里已经看出来了，`通过HbuliderX将RuleAPP运行到内置浏览器后，就可以看到访问页面的路径`。通过这些路径就可以找到对应的页面，就可以开始自己修改。**但是，这需要有网页知识和vue的基础才行。**

### 2.跳过简单的部分，来看看如下的配置。

![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "5.png")

5.png

这里提到了无数次的mid，这个就是typecho分类和标签的id，因为typecho的分类和标签都在同一个表，也就是typecho\_metas。其中就可以看到标签的mid。所以，其实这里，就是根据标签或者分类的mid，调用标签或者分类下的所有文章。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "6.png")

6.png

而文章发布的时候，是会让你选择分类或者输入标签的，比如 设置一个“幻灯”的标签作为轮播图数据来源，只要给文章的标签设置“幻灯”，然后去typecho\_metas表找到“幻灯”的mid，填入api.js，那么设置了“幻灯”这个标签的文章都会被获取图片，显示在app的首页轮播中。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "7.png")

6.png

![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "8.png")

6.png

### 3.图片上传方法的修改

在apijs中找到upload方法，可以看到如下，我默认开启的cos上传，但是还提供了其它上传方法，分别是本地上传，oss上传，远程ftp上传，这里需要根据自己的需求进行修改，比如大多数人都是用本地上传，那就要将上传方法切换为本地的。并且上传是需要后端接口配合的，具体的就去看这个教程：[RuleApi一键安装&更新脚本，傻瓜式配置，超快速运行](https://www.ruletree.club/archives/2786/)-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "9.png")

9.png

## manifest.json说明

对于RuleAPP而言，这个文件负责配置第三方登录，微信支付（对的，有且只有微信支付在这里配置），图标和启动图，还有打包相关。图标和启动图想必已经很直观了，这里就只说几个注意点。

### 1.第三方登录

这里有个注意点就是，`用的就开，用不上的别开，开了打包肯定报错`。QQ微博微信这三个的，都去各自的开发者平台申请appid等信息，每个APP都是不一样的，具体的各自的开发者平台都有教程。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "10.png")

10.png

### 2.微信支付

**请务必切记，支付宝不需要在这里进行配置！！！只有微信！！！只有微信！！！！**-
Ruleapp需要配置的支付就只有微信，其它的不需要开启，当然如果不用的话也不要开。如果还想要支持其它的支付，就只有自行二次开发了。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "11.png")

11.png

### 3.网页唤醒APP

找到如下图所示的位置，设置APP的UrlSchemes，这里自己定义一个英文的名称就好（小写），千万不要和我的一样，不然可能会直接在你的网页唤醒规则之树的APP（不过你免费打广告我也乐意）-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "8.png")

8.png

设置完成后，比如我设置的名称是ruleapp，那么在网页中，就可以通过超链接的或者js跳转的形式直接点击打开，比如如下代码：

    
       
       
        
        <a href="ruleapp://">打开app</a>
    
        
        
    
       
       

而这里，我提供了两个参数，一个是快捷登录（配合会员中心项目），一个是打开app文章阅读。

    
       
       
        
        ruleapp://?scan=快捷登录码
    
        
        ruleapp://?info=文章ID
    
        
        
    
       
       

无论是在网页上采用a标签或者js自动跳转，只要用户安装了app，都可以被唤醒。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "飞书20220414-050631.jpg")

飞书20220414-050631.jpg

推荐使用RuleUser项目，已经集成相关功能了。

[RuleUser安装及配置教程，让你的Typecho用户系统模块化](https://www.ruletree.club/archives/2990/)

### 4.首页数据推荐，专题等

用管理员账户登录APP，找到管理员中心，打开内容管理，选择已发布文章，就可以看到文章的推荐。然后回到内容管理，打开标签分类，就可以看到分类和标签的推荐，还可以设置缩略图。这里对应的就是首页的专题和推荐文章。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "20220423-150038.jpg")

20220423-150038.jpg

![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "20220423-150051.jpg")

20220423-150038.jpg

### 5.其它的设置

去看这个教程吧：[uniapp从基本配置到打包发布，详细流程](https://www.ruletree.club/archives/2894/)

## pages.json

这个文件定义了所有可以打开的页面，如果没有在里面定义，页面就无法开启。-
pages.json的底部定义了使用H5编译后打开的首页名称，和底部的四个选项卡图片和文字，可以根据自己的需求进行修改。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "12.png")

12.png

## APP在线更新及广告启动图

## 1.APP在线更新

在之前的教程里，安装完后端接口时，会提到一个apiResult.php文件，将这个文件放进typecho网站所在的目录，api.js里配置完WEB\_URL后，就可以通过apiResult.php文件管理app的用户更新和横幅广告。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "1.png")

1.png

版本的信息对应manifest.json文件中的版本设置，其实就是，你的最新版是什么信息，就在apiResult.php填入什么信息，程序会根据版本码判断，版本码低于最新的应用都会提示更新。`manifest.json里的版本号就是版本码`。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "2.png")

2.png

## 2.广告启动图

广告启动图是属于自己定义的APP启动图类型，它不等于官方的广告联盟启动图，也不等于APP的启动图。但是可以通过这种方式在启动图内推荐自己指定的内容，目前只在APP内生效，其它平台不会显示。具体的配置方式如下，留空则不显示。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "screenshot-20220710-153314.png")

screenshot-20220710-153314.png

## Typecho自定义字段

目前RuleApi已经集成了Typecho的自定义字段功能，而在APP代码内，暂时只通过这个功能实现了图文显示类型。因为我使用的是typecho小灯泡模板，所以我的类型字段是abcimg，可以个根据自己的模板进行修改，涉及的APP文件主要有以下三个。

    
       
       
        
        /page/home/home.vue
    
        
        /page/contents/contentlist.vue
    
        
        /page/manage/contents.vue
    
        
        
    
       
       

如果要改成自己的字段，可以先在可视化配置中心定义，然后在APP的api.js定义，如下图所示。

![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "screenshot-20220710-153822.png")

screenshot-20220710-153822.png

![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "screenshot-20220710-153833.png")

screenshot-20220710-153822.png

然后在从上述三个文件中搜索abcimg，改成自己所用typecho模板的字段和对应值。如果自己二次开发需要用到更多的自定义字段，可以去看RuleApi的接口文档。

## 二次开发部分

想要进行复杂的二次开发，需要系统性的学习vue和uniapp的官方教程，这个百度就有，不需要我多说。这里就提一些简单的。

## 1.图标的修改。

去看ColorUI的官方文档就好了：[点击进入](https://www.ruletree.club/go/aHR0cHM6Ly9kb2NzLnh6ZXUuY29tLyMv)

## 2.样式的修改

负责控制app全局样式的文件就是static/base.css，不过注意在uniapp中，一般像素大小是upx而不是px，其它的就和普通的css没区别了。

## 3.typecho模板自定义标签的兼容

一般来说，typecho的模板很多都会带一些自定义标签，就比如现在用的人很多的joe，以及我现在用的小灯泡模板。为了满足功能的需要，这些模板一般都会加自定义的，也就是markdown无法解析的标签对，所以如果遇到这种情况，就需要在RuleAPP里匹配模板的解析机制。

这很难吗？答案是不难，直接复制粘贴而已，因为模板只要有自定义标签，那就肯定有标签的解析方法，只要模板是开源的就可以找到，而且最主要的是，php的正则表达式和js没啥区别。以我的小灯泡模板为例，在/spimes/core/theme.php中，可以很清楚的看到如下代码：-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "11.png")

11.png

这里就是模板对自定义标签的解析，**只要不是代码加密的模板肯定可以找到！**

首先，这是我下图的分析：-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "12.png")

12.png

在RuleAPP中，解析文章内容的方法在page/content/info.vue，直接搜索markHtml找到对应的方法，这个方法就是用来处理标签解析的，比如我已经加好了解析小灯泡按钮的方法。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "13.png")

13.png

    
       
       
        
        text = text.replace(/\[button\ a=(.*?)\](.*?)\[\/button\]/sm,`<div class="btn_nt"><a class="btns" target="_blank" href="//$1">$2</a></div>`);
    
        
        
    
       
       

js的replace方法负责替换，第一个是正则表达式，直接复制PHP的就行，第二个是html代码，有网页开发基础就可以自己定义样式和内容。这段自定义标签有几个参数，用在那里，实际上每个typecho模板都肯定会写的，要做的就是复制粘贴，然后自己定义一下css。就这样，模板有几个自定义标签，就加个几行，就可以完成全部的解析，前提是找到你使用模板的标签解析方法，一般顺着function.php就可以找到。

同样的，评论也是如此。

## 小程序端编译

RuleAPP支持编译为微信小程序，QQ小程序，并在理论上支持所有小程序平台（如果编译出现问题，可以来群里反馈）。在编译为小程序的时候，由于图片大小和一些兼容性的限制，将部分本地图片引用改为远程。-
如首页专题的引用，可以将如下图所示的图片改为远程地址：-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "1.png")

1.png

注意，仅最新版支持上述操作，旧版本可能存在问题，具体可以加群了解。

## APP统计

uniapp官方是支持全平台统计的，所以无论怎样编译都可以被统计到，但前提是需要开启相关功能。主要都在mainifest.json，下图除了第一个勾，其它的都别动。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "1.png")

1.png

然后，就可以在统计配置中，选择想要统计的平台。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "2.png")

1.png

完成配置后，打包一个新版本，统计就会生效了。而查看统计则前往官方地址即可：

[uni统计,uni-app统计,多端统计](https://www.ruletree.club/go/aHR0cHM6Ly90b25namkuZGNsb3VkLm5ldC5jbi9ob21l)

## 最后

有啥遗漏的我再补充吧，可以直接在交流群里提意见。

点赞(23)

收藏

打赏

万水千山总是情，给个打赏行不行。 打赏 ![](https://image.cubox.pro/article/2022040909060542881/13170.jpg)

本文来自投稿，不代表本站立场，如若转载，请注明出处：https://www.ruletree.club/archives/2955/

[查看原网页: www.ruletree.club](https://www.ruletree.club/archives/2955/)