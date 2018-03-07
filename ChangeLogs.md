



## 更新记录

--

**Xiuno BBS 4.0.3 更新记录（发布时间：2018/3/6）：**

- 优化个人中心排版，更便于扩展。

- **手机注册插件**上线（登录、注册、重设密码、绑定手机号、更改手机号）。

- 验证码插件上线。

- 升级个人中心相关插件：通知，收藏，精华、编辑器。

- 全站升级插件（计划中）。

- 优化导航，更利于二次开发（计划中）

- 企业站插件（计划中）

- 积分插件（计划中）


补丁地址： 

[https://bbs.xiuno.com/down/v4.0.0-v4.0.3-patch.zip?v=2](https://bbs.xiuno.com/down/v4.0.0-v4.0.3-patch.zip?v=2)

覆盖后，手工编辑 conf/conf.php 中的 'version' => '4.0.3'

然后清空 tmp 目录（保留 tmp 目录）。

--

**Xiuno BBS 4.0.2 更新记录（2018/2/12）：**

- 修正 message() 函数风格丢失的问题

- 修正首页无权限主题过多页面短小的问题

- 缩减个人中心导航标题（我的主题 -> 主题）

- 版主操作改为 ajax dialog

- 兼容增强获取 CDN IP

- url() 函数从 XiunoPHP 移动到 BBS，方便自定义 URL

- JSON、我的回帖插件化

- 编辑历史插件上线

- 修正移动后缓存清理

- 添加了 .text-small 绝对大小，防止多次 .small 相对大小叠加的特别小字体。


补丁地址： 

[https://bbs.xiuno.com/down/v4.0.0-v4.0.2-patch.zip?v=4](https://bbs.xiuno.com/down/v4.0.0-v4.0.2-patch.zip?v=4)

覆盖后，手工编辑 conf/conf.php 中的 'version' => '4.0.2'

然后清空 tmp 目录（保留 tmp 目录）。


--

**Xiuno BBS 4.0.1 更新记录（2018/1/27）：**

- 修正查看我的回帖权限没有判断板块权限问题

- 修正 https_post() 在某些条件下发送 METHOD 为 GET

- 规范属性传参 pid="" tid="" 改为 data-pid="" data-tid=""

- 对 bootstrap.css 全局变量 :root{} 加入了 gray-100, gray-200...

- 修正一处 hook 名字笔误：header_meta_before.htm

- 增加了几处 hook（收藏插件需要）


**补丁地址：**

[https://bbs.xiuno.com/down/v4.0.0-v4.0.1-patch.zip](https://bbs.xiuno.com/down/v4.0.0-v4.0.1-patch.zip)

覆盖后，手工编辑 conf/conf.php 中的 'version' => '**4.0.1**'

然后清空 tmp 目录（保留 tmp 目录）。

--

**Xiuno 4.0.0 功能特性（2018/1/22）**

- 前端全面升级到 Bootstrap 4 正式版，响应式布局，适配手机，平板、电脑。

- JQuery 3.x

- 免费、收费插件系统

- 支持多语言，默认三种：简体、繁体、英文

- 支持 URL-Rewrite

- 支持 MySQL

- 支持各种 Cache：Memcached、YAC、Redis...

- 安全方面加强了参数的类型强制转换

- 性能方面优化了索引和缓存的粒度

- 默认上线了几套主题风格插件，供二次开发参考





## 一、什么是 Xiuno BBS 4.0？

它是一款国产、小巧、稳定、支持在大数据量下仍然保持高负载能力的轻论坛。它只有 20 多个表，源代码压缩后 1M 左右，运行速度非常快，处理单次请求在 0.01 秒级别，在有 APC、Yac、XCache 的环境下可以跑到 0.00x 秒，对第三方类库依赖少，作者认为它就像一辆纯手工打造的法拉利，动力强劲，没有一丝赘肉，方便部署和维护，是一个非常好的二次开发的基石。

Xiuno BBS 4.0 采用 Bootstrap 4 + JQuery 3 作为前端类库，全面支持移动端浏览器；后端 XiunoPHP 4.0 支持了 NoSQL 的方式操作各种数据库，这个版本是一个巨大的飞跃。

Xiuno 发音“修罗”，英文为 Shura，在佛教里面为六道之一"修罗道"，处于人道和天道之间。

Xiuno BBS 4.0 采用 MIT 协议发布，您可以自由修改、派生版本、商用而不用担心任何法律风险（修改后应保留原来文件的版权信息）。

## 二、漫长的等待：近两年

让各位同修们久等了，这次延迟的锅主要应该由 Bootstrap 4 来背（果断甩锅老外），我们跟踪它的版本经历了： alpha 3,4,5,6, beta1,2,3一年多，等到后面以为出不来了，还好虽然正式版终于出来了，正好同步发布！

而 Xiuno BBS 也经历了 1,2,3,4 的蜕变，期间我们也做过了很多尝试，最终产品形态和代码风格定型为当前形态。

后端采用自己的框架 XiunoPHP，面向对象封装底层，屏蔽 DB CACHE API 差异，应用层采用函数风格调用。

最后它看起来像这样：

```php

<?php
 
include "./xiunophp/xiunophp.min.php";
include "./model/user.func.php";
 
// 读取一个用户资料
$user = user_read(123);
 
// 更新一条用户资料
$r = user_update($uid, array('email'=>'xxx@gmail.com'));
 
// 删除一个用户
$r = user_delete($uid);
 
// 创建一个用户
$r = user_create(array('uid'=>1, 'gid'=>1, 'email'=>'xxx@gmail.com'));
 
// 查找一批用户
$userlist = user_find_by_gid($gid);
 
?>

```

没有 UserControl extends BaseControl 这样的继承，没有异常等高科技，回归本质，只是本本分分的写代码，让新人可以平滑的进入，而不像某些自称优美的框架，实际上学习成本高，远离了 PHP 简单高效的初衷。

因为后院的安定，使得我们可以把更多精力放到了产品的形态改造之上。

## 二、产品形态：**轻论坛**

在产品的形态方面，我们也摸索了很多种形式，最终我们定型为轻论坛，支持一维的板块，多维的主题分类（插件），自适应同时支持 PC 和手机，不搞全站无刷新。

最早我们针对手机和 PC 写了2套前端代码，发现后面维护相当的麻烦，一致性问题是个很严重的问题，随着时间的流失，当模板中的逻辑出现差异的时候，你不知道那边是对的。后来我们又针对宽屏尝试了三列布局，还有 AJAX 全站无刷新尝试...... 趟过了如此多的坑，最终我们发现 Bootstrap 4 给了我们最终的答案，响应式布局+跳转，平衡了用户体验和开发维护难度。（话说 Bootstrap 4 的 Flex 都应用都成熟了，Twitter 官方网站还一大坨 float style）

Xiuno BBS 4.0 正式版最后的 PC 界面：

![](http://bbs.xiuno.com/upload/attach/201801/1_NQK8RQPFKPKM2QV.png)

手机版：

![](http://bbs.xiuno.com/upload/attach/201801/1_545JH364FBEWZUE.png)

## 三、前端：Bootstrap 4 全球生态

我们遵照 Bootstrap 4 的 UI 规范，基本上没有写过 style，尽量用 class 搞定。另外 flex 布局的加入，确实方便了很多。比如页脚底部对齐，在语义不变的情况下很轻松就搞定了。Bootstrap 4 的全球生态链未来肯定也会惠及 Xiuno，这点是毋庸置疑的。比如插件的编写可以直接使用 BS 的现成的控件和引入基于 BS 开发的模块。

来看看 Bootstrap 带来了哪些方便的特性：

**3.1 Flex 布局，.col 自适应宽度：**

![](http://bbs.xiuno.com/upload/attach/201801/1_SJCS97VP8DA5N4U.png)  

https://getbootstrap.com/docs/4.0/layout/grid/

**3.2 标准化控件：**

![](http://bbs.xiuno.com/upload/attach/201801/1_KRYXCABADKY2E2W.png)

更多请自行了解：https://getbootstrap.com/docs/4.0/getting-started/introduction/

在使用 SCSS 后制作风格效率大大提高，例如红色模板，只花了大约十分钟时间：

![](http://bbs.xiuno.com/upload/attach/201801/1_MWZKU7EG8D3PC3T.png)

此次同步发布了三套免费模板：

![](http://bbs.xiuno.com/upload/attach/201801/1_X9QVS7EH67QUEHZ.png)

分别对应三种不同的风格制作方式， 最简单的 css overwrite，到 SCSS 编译，详细的教程随后会出来，有经验的打开插件目录看下就懂了。另外理论上还有未来海量的 BS4 全球生态带来的各种组件和风格可用。

## 四、性能方面

Xiuno 最早诞生就是为了解决负载问题，这个基因不会变，2.1 用力过猛，4.0 往回收了收，更多让位给了易读性和可维护性。性能和安全、复杂度是矛盾的，我们尽量降低业务、代码、数据库设计等多方面的复杂度。在表的设计上，非常注重索引和缓存的使用。这里面有一个平衡性问题，经过了反复调整，最后找到了一个比较完美的尺度。

比如，拿置顶帖这个功能来说，一般会这么设计表结构

```sql

CREATE TABLE bbs_thread(
    fid int(10),    
    tid int(10),
    top tinyint(3),
    KEY(fid, tid),
    KEY(fid, top,tid)
);

```

查询的时候，一条SQL搞定：

```sql
	
SELECT * FROM bbs_thread WHERE fid=1 ORDER BY top DESC, tid DESC LIMIT 0, 10;

```

简单粗暴是不是？但是在数据量特别大，并发请求高的时候，这样就会有性能问题。假定数据量有 1000w，置顶帖子不超过10个，为了照顾这 10 个帖子，我们要对 1000w 主题进行排序，是不是太浪费？所以正确的做法是，小表。

```sql

CREATE TABLE bbs_thread_top(
        fid int(10),
        tid int(10),
        top tinyint(3),
        KEY (fid)
)
SELECT * FROM bbs_thread WHERE tid IN(SELECT tid FROM bbs_thread_top);
SELECT * FROM bbs_thread WHERE fid=123 ORDER BY tid DESC LIMIT 0, 10;
# PHP 合并两条结果

```

我们用一个小表来降低大表的负载，虽然业务逻辑会变的复杂一点，但是很好的照顾到了性能。

SQL 并不是写的越长水平越高，看到 DBA show SQL 语句，程序员如果也盲从就暴漏智商了，要明白你们不是一群生物，需求不一样。

像这样的设计原则和平衡，在 Xiuno 里随处可见。

另外我们坚持用 SELECT * 而不写长条字段，也是有原因的，因为我们可以在中间加入缓存。比如用户数据，我们按条去，按条缓存，在开启 memcached, yac 后，中间的这些 SQL 都消失了。

```php

// 从缓存中读取，避免重复从数据库取数据，主要用来前端显示，可能有延迟。重要业务逻辑不要调用此函数，数据可能不准确，因为并没有清理缓存，针对 request 生命周期有效。
function user_read_cache($uid) {
        global $conf, $g_static_users;
        if(isset($g_static_users[$uid])) return $g_static_users[$uid]
        // 游客
        if($uid == 0) return user_guest()
        if($conf['cache']['type'] != 'mysql') {
                $r = cache_get("user-$uid");
                if($r === NULL) {
                        $r = user_read($uid);
                        cache_set("user-$uid", $r);
                }
        } else {
                $r = user_read($uid);
        }
        $g_static_users[$uid] = $r ? $r : user_guest()
        return $g_static_users[$uid];
}

```

在 PHP 的性能方面，要注意的也很多，比如要尽量减少 IO 密集型和 CPU 密集型相关函数的使用，循环的深度和次数等等，有机会我会展开说。

## 五、安全方面

不用再担心被 Webshell，SQL 注射等这些问题困扰。Xiuno 在安全方面一直很注重，经过了多年的实战检验，作者经常接触安全圈，熟悉常见攻击手段，国内知名社区看雪安全论坛采用的就是 Xiuno BBS 4.0，目前还未出现过什么安全问题。Xiuno 的参数经过了严格的类型过滤，拼接 SQL 的相关函数也严格进行了转义，正常写是不会有什么安全问题的。

但是，安全问题是一个综合问题，框架层面只能保证最基础的，最终还是要靠安全意识来保障，比如弱密码，越权等问题，信息泄露，旁注等，谁也不敢说自己是百分之百安全，不能说你家防盗门结实就是安全的，窗户，通风管道，都有可能成为突破口。插件可能会成为一个软肋，不要随便安装第三方作者开发的插件，除非第三方作者有较好的安全意识，或者插件被官方认证过。

以下为参数过滤、数据库传参的范例代码：

```php

<?php
 
include './xiunophp/xiunophp.min.php';
 
// 安全的参数获取方式：
$uid = param('uid', 0);     //  整形类型，默认 0
$name = param('name', '');       // 默认为字符串，并且默认会做 XSS 过滤
$arr = param(array(0), 0);     // 数组类型，元素为整形，默认 0
$word = param_word('word', 32);     // 默认获取单词类型，长度 32
$s = param_base64('filedata', 1000000);    // base64 类型的数据
$arr = param_json('arr');     // json 格式的数据
 
// 送入 db 层
db_create('user', array('uid'=>123, 'email'=>'xxx@gmail.com'));
db_update('user', array('uid'=>123), array('email'=>'yyy@gmail.com'));
db_delete('user', array('uid'=>123)); 
 
?>

```

## 六、插件：支持收费插件

增强了多维主题分类插件，支持了强制，默认等功能：  

![](http://bbs.xiuno.com/upload/attach/201801/1_BF4VHF53JQ4TBR9.png)  

支持了标签颜色：

![](http://bbs.xiuno.com/upload/attach/201801/1_B68UFPYJSDEJ2CD.png)

**收费插件上线，开发者们可以撸起袖子开干了！！！**

提交插件：http://plugin.xiuno.com/plugin.htm

开发文档：https://bbs.xiuno.com/thread-13108.htm

## 七、对 HTTPS / CDN 支持

部署 https 不需要修改任何代码和配置。

对市面各种 CDN 兼容性完好，同时感谢可靠云免费给修罗官方提供支持，使用这段时间来很稳定，免费还支持 HTTPS。

如何配置HTTPS: http://bbs.xiuno.com/thread-18004.htm

## 八、未来：不可知

从刚开始只需要考虑 IE6 到浏览器百花齐放，到 CHROME 一统江湖，到移动端大潮，到 AI、区块链 ......  

未来是 React 的？还是 VUE ? 还是小程序？还是 Web Asambley？还是 C++11 / QT？go ? 还是其他？

这个问题我想时间会给我们答案，目前重要的是，我们要把眼前的事情做到足够好。

感谢各位开发者和站长的支持，不厌其烦的反馈八哥，给修罗提建议，没有你们，就没有修罗。

最后感谢 CCTV，不敢想象假如没有 CCTV，我们该如何树立正确的人生观世界观？如何正确的编写代码？

axiuno

2018/1/21

--

**站长交流群：**

474834730

**开发者群：**

2759536

--

## **常见问题：**


**如何升级 Xiuno BBS 4.0 beta 版？**

如果是 Xiuno BBS 4.0 beta 版本，升级步骤很简单：

1. 下载后，解压

2. 备份一下 conf/smtp.conf.php   （可以改个名字）

3. 覆盖整个文件夹

4. 清空 tmp, plugin 目录（自己定制的插件目录改个目录名）

5. 打开页面，CTRL+F5 （如果有CDN，清一下CDN缓存，或者修改下 conf/conf.php static_version 的值）

升级完毕。

**如何升级原来的插件？**

用脚本跑一下，批量替换下就差不多了。

https://bbs.xiuno.com/thread-19573.htm

**发现详情页引用的头像大小偏大？**

执行以下SQL：

update bbs_post set message_fmt=replace(message_fmt,'avatar-xs','avatar-1');


