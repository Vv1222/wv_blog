---
layout: post
title:  "GitHub+Jekyll个人博客添加访问量和gitment评论"
date:   2019-01-03 22:50:22 +0800
categories: blog
---



> * 访问量：[不蒜子][1]
> * 评论：**gitment**

---

## 1、 添加访问量

使用不蒜子，在需要显示访问量的页面添加以下两段代码即可。

```
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<span id="busuanzi_container_site_pv">本站总访问量<span id="busuanzi_value_site_pv"></span>次</span>
```

---

## 2、 添加gitment评论

gitment是基于github issues的评论系统，具体步骤如下：

> ① 申请 Github OAuth Application

右上角GitHub头像-Settings-Developer settings-OAuth Apps-Register a new OAuth application
<br/>
填写注册信息
<br/>
Application name 可以随意写


Homepage URL 写自己博客的地址就行


Application description 随意写


**Authorization callback URL** 这里要写自己GitHub Pages的URL，或者域名



注册完成后会得到一个Client ID 和一个Client Secret


> ② 调用gitment

在_config.yml文件里添加如下代码，修改四个“此处”的地方即可。

```
#gitment

gitment:
  enable: true
  mint: true        # RECOMMEND, A mint on Gitment, to support count, language and proxy_gateway
  count: true       # Show comments count in post meta area
  lazy: false       # Comments lazy loading with a button
  cleanly: false    # Hide 'Powered by ...' on footer, and more
  language:         # Force language, or auto switch by theme
  github_user:  # 此处 - Your Github ID
  github_repo:  # 此处注意 - The repo you use to store Gitment comments
  client_id:    # 此处 - Github client id for the Gitment
  client_secret: # 此处 - Github access secret token for the Gitment
  proxy_gateway: # Address of api proxy, See: https://github.com/aimingoo/intersect
  redirect_protocol: # Protocol of redirect_uri with force_redirect_protocol when mint enabled
```

然后在_layouts/下的post.html添加如下代码：

```
<div id="gitmentContainer"></div>
<link rel="stylesheet" href="https://jjeejj.github.io/css/gitment.css">
<script src="https://jjeejj.github.io/js/gitment.js"></script>
<script>
var gitment = new Gitment({
    id: '{{ page.title }}',
    owner: 'Github ID',
    repo: 'The repo you use to store Gitment comments',
    oauth: {
        client_id: 'Github client id for the Gitment',
        client_secret: 'Github access secret token for the Gitment',
    },
});
gitment.render('gitmentContainer');
</script>
</div>
```

repo：评论通过issues存放，可以新建一个仓库，或者直接用博客所在的仓库

> ③ 初始化评论

调用成功后，需要到每一篇文章下初始化评论。
在初始化前会提示Error: Comments Not Initialized,登陆自己的GitHub后点击Initialize Comments，就可以了。

> ④ 错误解决

- **登陆报错Object ProgressEvent**
原作者的服务器没有再维护了，如果引用的是原作者的链接出现这个问题替换一下就可以了。
代码如下：
```
<link rel="stylesheet" href="https://jjeejj.github.io/css/gitment.css">
<script src="https://jjeejj.github.io/js/gitment.js"></script>
```
- **Error：validation failed**
issue的标签label有长度限制，labels的最大长度限制是50个字符。
在_layouts/下的post.html刚刚添加的代码修改： 

```
id: “<%=url%>”改成id: '{{ page.title }}'
如果本来没有则加上id: '{{ page.title }}'即可
```
- **明文密码风险**
直接把Client Secret写在页面不知道会有啥风险不，替代方案新建个小号换掉这里的id和secret，反正博客也没人看就先不折腾了。。。

 [1]: http://busuanzi.ibruce.info/
