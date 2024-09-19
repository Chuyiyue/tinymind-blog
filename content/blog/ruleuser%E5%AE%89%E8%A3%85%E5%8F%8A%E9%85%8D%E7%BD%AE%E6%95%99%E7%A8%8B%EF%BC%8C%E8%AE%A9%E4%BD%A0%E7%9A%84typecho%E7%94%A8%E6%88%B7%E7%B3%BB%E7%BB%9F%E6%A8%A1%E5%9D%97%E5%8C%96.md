---
title: RuleUser安装及配置教程，让你的Typecho用户系统模块化
date: 2024-09-19T13:00:52.086Z
---


[www.ruletree.club](https://www.ruletree.club/archives/2990/)大AVLv.3 说道：

RuleUser作为原本计划中的第三环，已经正式出炉1.0版本，它的目的很简单，通过API的方式完全接管typecho的用户系统，让Typecho网站拥有一个独立会员中心的同时，还可以将前台用户的操作全部API化。不过这篇文章主要负责讲述RuleUser的安装和配置过程，希望能让每一个用户能够简单方便的使用RuleUser升级自己网站的用户系统。

注意：对于安装，配置，使用中出现的任何问题，都可以加群询问（都是免费的，只要在线我都会回答，没有收钱的说法）-
QQ群：776176904

### 写在前面，不要觉得配置很困难，实际上就是复制粘贴而已，代码都是现成的。

另外，为了让各位快捷使用，我已经做好了如下模板的配置，可以直接加群在群文件下载，如果需要支持更多模板，也可以加群来提交。

    
       
       
        
        JOE模板
    
        
        小灯泡Spimes 5.0版本
    
        
        
    
       
       

RuleUser的扫码功能是搭配这个开源免费的APP实现的，而且很多数据和操作全都同步，感兴趣可以了解一下：[点击进入](https://www.ruletree.club/go/aHR0cHM6Ly9leHQuZGNsb3VkLm5ldC5jbi9wbHVnaW4|aWQ9NjkwOQ==)

## 详细介绍及下载地址：

可前往之前的文章：[Typecho独立会员中心，前后端分离，充值付费功能集成，APP扫码登录](https://www.ruletree.club/archives/2979/)

## 安装教程：

1.RuleUser是基于接口的前后端分离应用，所以首先需要安装RuleApi，这是一个typecho的综合性接口，可以直接满足后续无论是前后端分离，手机客户端，微信小程序等一系列的支持，通过下方的文章进行安装，遇到的一切问题，都可以在群里询问。

[RuleApi一键安装&更新脚本，傻瓜式配置，超快速运行](https://www.ruletree.club/archives/2786/)

2.安装完成RuleApi后，在typecho网站的根目录新建一个文件夹，将下载的RuleUser上传到其中解压，比如我就是新建一个叫做ruleuser的文件夹，这是解压后的效果。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "1.png")

1.png

3.编辑目录下的configs.js文件，可以看到如下信息，首先重点配置API\_URL和userIndex，这个分别对应RuleApi接口地址和RuleUser的访问目录，比如我上一步里就把它放在ruleuser文件夹，所以userIndex就是ruleuser。其它的信息就根据注释配置吧。（`这里注意，基础版是不需要管授权码的，完全免费！！`）-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "2.png")

2.png

4.访问路径，出现登录界面，安装就完成了。这里可以去查看我网站的效果，或者直接体验我网站的登录注册（首页有cdn缓存，可以跳过）。

[规则之树-会员中心](https://www.ruletree.club/ruleuser/)

## 二次开发说明：

源码的CSS是可以随意修改的，所以可以自行美化，而具体的功能也可以通过参考RuleAPi的接口文档，配合js的知识来实现。-
[RuleApi接口文档](https://www.ruletree.club/go/aHR0cHM6Ly9kb2NzLmFwaXBvc3QuY24vcHJldmlldy8xMmUyZDBlN2FiMmY4NzM4LzljN2ZkMTg3NzE4ODRjYjI=)

## 会员系统接管教程（不接管也没事，看自己心情就好）：

各位访问规则之树的时候，会发现规则之树可以在网站内进行登陆注册，并且从点赞，收藏，打赏，评论都被API接管了。所以接下来的内容，就是指导各位用户如何使用RuleUser接管用户操作。方案有两种，第一种是php实现，第二种是js实现。

在这之前，需要在typecho模板中引入RuleUser，只需要修改模板的footer.php文件，在</body>的上方，加入如下代码（ruleuser是我前面步骤自定义的文件夹名称，代表RuleUser所在目录）：

    
       
       
        
        <script src="/ruleuser/configs.js?v1.02"></script>
    
        
        <script src="/ruleuser/main/RuleUser.js?v1.02"></script>
    
        
        <script>
    
        
            loadPostBtn(<?php echo $this->cid; ?>);
    
        
            loadPostShop(<?php echo $this->cid; ?>)
    
        
        </script>
    
       
       

然后，在文章模板，post.php合适的位置（一般是文章内容底下，加入如下代码）：

    
       
       
        
        <div id="RuleUser-PostShop"></div>
    
        
        <div id="RuleUser-PostBtn"></div>
    
        
        
    
       
       

这样，就可以调用出文章插入的付费商品和操作按钮，截图如下：-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "7.png")

7.png

另外，会员的登录注册，可以参考如下方式接管，`重点只在onclick中`，本质上就是绑定点击事件：

    
       
       
        
        <button type="button" onclick="UserLogin()">登录</button>
    
        
        <button type="button" onclick="UserRegister()">注册</button>
    
        
        <button type="button" onclick="UserForgot()">找回密码</button>
    
        
        <button type="button" onclick="UserScan()">扫码登录</button>
    
        
        <button type="button" onclick="UserQuit()">退出登录</button>
    
        
        
    
       
       

举例就是，typecho默认的登录链接如下：

    
       
       
        
        <a href="<?php $this->options->adminUrl('login.php'); ?>"><?php _e('登录'); ?></a>
    
        
        
    
       
       

改为如下，就可以被RuleUser接管，本质上就是把href的内容改成javascript:;，然后绑定onclick事件。

    
       
       
        
        <a href="javascript:;" onclick="UserLogin()" ><?php _e('登录'); ?></a>
    
        
        
    
       
       

这里还提到一点就是，在文章里唤醒app并打开文章，代码参考如下，这里要配合RuleAPP使用。

    
       
       
        
        <a href="javascript:;" onclick="openApp('?info=<?php echo $this->cid; ?>')">在APP中阅读</a>
    
        
        
    
       
       

## 方案一：php接管（简单快捷，需要PHP基础）

此种方法将完全遵守typecho原有的模块开发规范，配置完成后不需要对模板大弧度修改，可以保证一些新手用户不会把模板弄坏。

1.在typecho模板的function.php文件底部，增加如下代码：

    
       
       
        
        function toLogin($token,$uid){
    
        
            //  如果不存在就写入 Cookie
    
        
            Typecho_Cookie::set('__typecho_token', $token);
    
        
            Typecho_Cookie::set('__typecho_token_uid', $uid);
    
        
            if($uid==0){
    
        
                Typecho_Cookie::set('__typecho_token', 0);
    
        
                Typecho_Cookie::set('__typecho_token_uid', 0);
    
        
                Typecho_Cookie::delete('__typecho_token');
    
        
                Typecho_Cookie::delete('__typecho_token_uid');
    
        
            }
    
        
        }
    
        
        function getLogin(){
    
        
            if (empty($recording = Typecho_Cookie::get('__typecho_token'))) {
    
        
                
    
        
                return 0;
    
        
            } else {
    
        
                $uid = Typecho_Cookie::get('__typecho_token_uid');
    
        
                return $uid;
    
        
            }
    
        
        }
    
        
        function quitUser(){
    
        
            Typecho_Cookie::set('__typecho_token', 0);
    
        
            Typecho_Cookie::set('__typecho_token_uid', 0);
    
        
            Typecho_Cookie::delete('__typecho_token');
    
        
            Typecho_Cookie::delete('__typecho_token_uid');
    
        
        }
    
        
        //根据字段获取用户信息
    
        
        function userInfo($value,$uid)
    
        
        {
    
        
            $db   = Typecho_Db::get();
    
        
            $prow = $db->fetchRow($db->select($value)->from('table.users')->where('uid = ?', $uid));
    
        
            $text = $prow[$value];
    
        
        
    
        
            return $text;
    
        
        } 
    
        
        
    
       
       

2.修改模板的header.php(头部文件)，将下方代码：

    
       
       
        
        <?php if (!defined('__TYPECHO_ROOT_DIR__')) exit; ?>
    
        
        
    
       
       

修改成：

    
       
       
        
        <?php if (!defined('__TYPECHO_ROOT_DIR__')) exit; 
    
        
        if(isset( $_POST["token"])){
    
        
            $token =  $_POST["token"];
    
        
            $uid =  $_POST["uid"];
    
        
            toLogin($token,$uid);
    
        
        }
    
        
        if(isset( $_GET["quit"])){
    
        
            toLogin(0,0);
    
        
        }
    
        
        
    
        
        ?>
    
        
        
    
       
       

3.完成上述操作后，可通过如下的方式判断typecho的登录状态，用于替换模板中的登录状态判断：

    
       
       
        
        <?php if(getLogin()!=0): ?>
    
        
        //已登录
    
        
        <?php else : ?>
    
        
        //未登录
    
        
        <?php endif; ?> 
    
        
        
    
       
       

用户相关的标签调用如下：

    
       
       
        
        <?php echo getLogin(); ?> //输出会员ID
    
        
        <?php echo userInfo('mail',getLogin()); ?> //会员邮箱 
    
        
        <?php echo userInfo('name',getLogin()); ?> //会员用户名
    
        
        <?php echo userInfo('screenName',getLogin()); ?> //会员昵称
    
        
        <?php echo userInfo('url',getLogin()); ?> //会员网址
    
        
        <?php echo userInfo('group',getLogin()); ?> //会员用户组
    
        
        <?php echo userInfo('assets',getLogin()); ?> //会员资产
    
        
        //总之数据库user表里所有的字段都可以调出来
    
        
        
    
       
       

这样就可以去替换并灵活搭配来在php层面实现用户的数据调用。

4.对于评论的接管，首先需要f12查看typecho评论的表单。以我自己的为例，可以看见评论form表单的id叫做new\_comment\_form，实际上如果没有，可以自己编辑模板的comments.php文件，自己修改命一个id。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "3.png")

3.png

然后，编辑comments.php文件，找到提交表单的按钮。以如下代码为例：

    
       
       
        
        <button type="submit" class="submit"><?php _e('提交评论'); ?></button>
    
        
        
    
       
       

将type="submit"改为type="button"，然后新增点击事件，变成如下：

    
       
       
        
        <button type="button" class="submit" onclick="addComments(<?php echo $this->cid; ?>,'#new_comment_form')"><?php _e('提交评论'); ?></button>
    
        
        
    
       
       

重点就是这句：

    
       
       
        
        onclick="addComments(<?php echo $this->cid; ?>,'#new_comment_form')"
    
        
        
    
       
       

可以看到new\_comment\_form加了#号，其实就是form标签的id名称，做完这些修改之后，如果用户登录，那么评论将通过api提交，如果用户没有登录，那么评论将会走typecho自带模式。

然后找到评论的文本框textarea代码，类似下图这样，添加id为RuleText。-
![](https://image.cubox.pro/article/2022040909060542881/13170.jpg "2.png")

2.png

## 方案二：js方式（需要有JS基础）

1.对于用户登录的区域，可以自己创建js文件，或者在footer.php新建script标签，写入如下代码，判断登录状态。

    
       
       
        
        if(localStorage.getItem("token")){
    
        
          //已登录
    
        
        }else{
    
        
          //未登录
    
        
        }
    
       
       

举个例子，拿小灯泡一个老版本模板做范例，给定一个登陆的区域：

    
       
       
        
        <div class="login" id="login">
    
        
        </div>
    
       
       

js里就可以这么写：

    
       
       
        
        var html=``;
    
        
        if(localStorage.getItem("token")){
    
        
            var userData = JSON.parse(localStorage.getItem('userinfo'));
    
        
            if(userInfo.screenName){
    
        
                    name = userInfo.screenName;
    
        
                }
    
        
            html = `
    
        
            <a href="javascript:;" id="auStats" class="dropdown-toggle"><img src="${userData.avatar}" width="32px" height="32px" class="navtar" >
    
        
            ${userData.name}
    
        
            </a>
    
        
            <div class="austats" id="aus">
    
        
            <ul>                        
    
        
            <li><a href="javascript:;"  onclick="UserQuit()"><i class="icon iconfont icon-shibai"></i>退出登录</a></li>                            
    
        
            </ul>
    
        
            </div>                    
    
        
            `
    
        
        }else{
    
        
            html=`
    
        
            <i class="icon iconfont icon-zengjia"></i><a href="javascript:;" onclick="UserLogin()"><?php _e('登录'); ?></a>
    
        
            `;
    
        
        }
    
        
        $("#login").html(html);
    
        
        
    
       
       

通过localStorage的userinfo这个字段，就可以拿出所有用户信息。实在看不懂可以直接右键我网站的首页，直接拖到尾部，相信有点js基础的人就能看懂了。

2.而对于其它位置的功能，毕竟都已经有js基础了，可以参考我的RuleAPi接口文档自己对接。

[点击进入](https://www.ruletree.club/go/aHR0cHM6Ly9kb2NzLmFwaXBvc3QuY24vcHJldmlldy8xMmUyZDBlN2FiMmY4NzM4LzljN2ZkMTg3NzE4ODRjYjI=)

## 前端提交js参考：

这里我公开一些我写的代码，之后可以自己参考进行增加或者修改。

1.用户登录：

    
       
       
        
        function toLogin(){
    
        
            var username = $("#username").val();
    
        
            var userpass = $("#userpass").val();
    
        
            if(username==""||userpass==""){
    
        
                layer.msg("请输入正确的参数", {icon: 2});
    
        
                return false;
    
        
            }
    
        
            var data = {
    
        
                name: username,
    
        
                password: userpass,
    
        
            }
    
        
            var index = layer.load(1, {
    
        
              shade: [0.4,'#000']
    
        
            });
    
        
            
    
        
            $.ajax({
    
        
                type : "post",
    
        
                data:{"params":JSON.stringify(API.removeObjectEmptyKey(data))},
    
        
                url : API.userLogin(),
    
        
                dataType: 'json',
    
        
                success : function(result) {
    
        
                    layer.close(index); 
    
        
                    if(result.code==1){
    
        
                        layer.msg("登录成功！", {icon: 1});
    
        
                        //保存用户信息
    
        
                        localStorage.setItem('userinfo',JSON.stringify(result.data));
    
        
                        localStorage.setItem('token',result.data.token);
    
        
                        //下面负责和typecho同步登录状态
    
        
                        typechoLogin(result.data.token,result.data.uid,1);
    
        
                        if(TypechoUserLogin==0){
    
        
                            var timer = setTimeout(function() {
    
        
                                location.reload();
    
        
                                clearTimeout('timer')
    
        
                            }, 1000)
    
        
                        }
    
        
                    }else{
    
        
                        layer.msg(result.msg, {icon: 2});
    
        
                    }
    
        
                },
    
        
                error : function(e){
    
        
                    layer.close(index);
    
        
                    layer.alert("请求失败，请检查网络", {icon: 2});
    
        
                }
    
        
            });
    
        
        }
    
        
        
    
       
       

2.提交评论：

    
       
       
        
        function addComments(cid,sumbit){
    
        
               //判断用户信息是否存在
    
        
            var token;
    
        
            if(localStorage.getItem("token")){
    
        
                token = localStorage.getItem("token");
    
        
            }else{
    
        
               //不存在就走typecho默认的评论登录
    
        
                $(sumbit).submit();
    
        
                return false;
    
        
            }
    
        
               //上级评论id，typocho模板基本都是下面这个id
    
        
            var coid = $("#comment-parent").val();
    
        
            var text =  $("#RuleText").val();
    
        
            if(coid==""||cid==""||text==""){
    
        
                layer.msg("请输入正确的参数", {icon: 2});
    
        
                return false;
    
        
            }
    
        
            var data = {
    
        
                "cid":cid,
    
        
                "parent":coid,
    
        
                "text":text,
    
        
            }
    
        
            var index = layer.load(1, {
    
        
              shade: [0.4,'#000']
    
        
            });
    
        
            
    
        
            $.ajax({
    
        
                type : "post",
    
        
                url: API.setComments(),
    
        
                data:{
    
        
                    "params":JSON.stringify(API.removeObjectEmptyKey(data)),
    
        
                    "token":token
    
        
                },
    
        
                dataType: 'json',
    
        
                success : function(result) {
    
        
                    layer.close(index); 
    
        
                    if(result.code==1){
    
        
                        layer.msg("发布成功！", {icon: 1});
    
        
                        var timer = setTimeout(function() {
    
        
                            location.reload();
    
        
                            clearTimeout('timer')
    
        
                        }, 1000)
    
        
                        
    
        
                    }else{
    
        
                        layer.msg(result.msg, {icon: 2});
    
        
                    }
    
        
                },
    
        
                error : function(e){
    
        
                    layer.close(index); 
    
        
                    layer.alert("请求失败，请检查网络", {icon: 2});
    
        
                }
    
        
            });
    
        
        }
    
        
        
    
       
       

## 补充一点

方案一的好处是不会对模板进行大改，可以很方面的接管，而且完全按照php的标签规范，但是坏处是如果挂了cdn就会导致登录状态被缓存，就比如我自己网站的首页。而且性能的提升不如纯js前后端分离。

方案二的好处是完全js前后端分离，无论是用户交互还是网站性能都可以依靠js达到很高的提升，缺点就是需要有js的基础知识，对个人能力有要求，并且如果碰到复杂的模板，改起来也话时间。

## 最后

文章中的功能和配置可能会因为RuleUser的升级和完善发生更改，并不等于最终功能。我是一个很有耐心的人，如果出现了问题可以加群直接发言，我可能忙不在线，但是上线了会很快回复，都是免费的，请放心。![](https://image.cubox.pro/article/2022040909060542881/13170.jpg)。

希望typecho越来越好。

点赞(30)

收藏

打赏

万水千山总是情，给个打赏行不行。 打赏 ![](https://image.cubox.pro/article/2022040909060542881/13170.jpg)

本文来自投稿，不代表本站立场，如若转载，请注明出处：https://www.ruletree.club/archives/2990/

[查看原网页: www.ruletree.club](https://www.ruletree.club/archives/2990/)