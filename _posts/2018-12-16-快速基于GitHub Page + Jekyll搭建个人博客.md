---
layout:          post
title:           快速基于GitHub Page + Jekyll搭建个人博客
subtitle:        利用现成可拉取的模版及可自定义个性化风格
date:            2018-12-16
author:          rookflying
header-img:        img/github_jekyll/background.jpg
catalog:         true
tags:
    - Jekyll
    - github
---

> 本文适用于无需深入了解jekyll原理，只求快速看到成效的读者- -

# 1. 环境搭建

## 1.1 Mac or Linux

Mac需先安装Xcode。

安装rvm，rvm是个ruby版本管理器，用来装各种版本的ruby的。

```
curl -L https://get.rvm.io | bash -s stable
```

安装好后会提示 source ~/.bash_profile 将rvm添加到环境变量中。也可以关闭，重新打开一个terminal，新开的terminal会更新环境变量。

接着使用　rvm use 来使用具体版本的ruby。

```
rvm use 2.4.1
```

如果发现没有可用的指定版本的ruby，会提示你安装，按着提示命令敲就好。安装完之后会自动切换到该版本的ruby环境。

接着使用gem安装jekyll，gem是ruby的包管理器，类似于py的pip？

```
gem install jekyll
```

## 1.2 Windows

传送门：[Windows安装jekyll](https://blog.csdn.net/qiujuer/article/details/44620019)

# 2. 拉取模版本地测试


[repo地址](https://github.com/rookflying/rookflying.github.io)

先fork到自己的仓库，然后克隆到本地。克隆可以走https协议，也可以走ssh协议。以后push的时候，https协议每次都需要输入用户名和密码，ssh协议则需要在服务端配置公钥，不用每次输入口令。ssh协议速度快些。

该模版用到了两个插件，因此克隆到本地之后，需要在本地环境安装这两个插件：

```
gem install jekyll-paginate
gem install jekyll-sitemap
```

安装完之后就可以在本地测试了：

```
jekyll serve
```

默认端口是4000，因此现在可以访问http://127.0.0.1:4000查看效果了。本地测试好像并不支持https。

# 3. 在github上部署

github支持自动利用jekyll生成站点，因此部署非常简单。。只需要改一下repo的名字。。

在github上将刚刚fork的repo名字给改了，改成xxx.github.io形式，xxx是github用户名。接着就可以访问xxx.github.io了（可能会有几分钟的缓冲时间）。

github是按照master分支来生成站点的，因此确保更新的内容merge到master，或者直接push到master，才能看到更新的内容。

# 4. 全局配置文件_config.yml

这个站点的配置是通过这个全局配置文件来的，这个配置文件实际上就是定义一堆全局变量，站点里的其他文件可以访问到这些全局变量来渲染出不同的静态网页。因此实际上并不需要关心站点的项目布局，只需要关注这个配置文件就好了。例如下面的一些个性化内容：

```
# Site settings
title: rookflying's blog
SEOTitle: rookflying's blog
header-img: img/home.jpg
email: cpeng2424@163.com
description: "Somebody has to win"
keyword: "rookflying"
url: "https://rookflying.com"          # your host, for absolute URL
baseurl: ""      # for example, '/blog' if your blog hosted on 'host/blog'
github_repo: "https://github.com/rookflying/rookflying.github.io.git" # you code repository
```

可以看到配置文件的格式就是简单的 变量名：变量值。可以自行修改，本地测试查看修改结果，这上面的都是一些个性化的内容。

## 4.1 侧边栏

```
# Sidebar settings
sidebar: true                           # whether or not using Sidebar.
sidebar-about-description: "Somebody has to win"
sidebar-avatar: /img/avatar.jpeg      # use absolute URL, seeing it's used in both `/` and `/about/`



# SNS settings
RSS: false
github_username:        rookflying
codeforces_username:    DamJoker
```

sidebar:true 表示使用侧边栏，接着是一段文字和头像的设置。侧边栏下面还可以设置到其他平台的超链接，这里我只设置了github和codeforces的，可以自行添加，如添加知乎的：

```
zhihu_username:     xxxxx
```

接着在/_layouts/page.html里合适的地方添加如下代码（ctrl+f搜索codeforces__name的对应地方）：

![](https://github.com/rookflying/rookflying.github.io/blob/master/img/github_jekyll/html_code.png?raw=true)

页面下方也有超链接，也往_includes/footer.html里添加上面这段代码。

关于标签的配置如下：

```
# Featured Tags
featured-tags: true                     # 是否使用首页标签
featured-condition-size: 0              # 相同标签数量大于这个数，才会出现在首页
```

## 4.2 评论系统

评论用的是gitalk插件，代码已嵌入写好，只需要修改配置文件。

```
# Gitalk
gitalk:
  enable: true    #是否开启Gitalk评论
  clientID: xxxxxxxxxxxx                         #生成的clientID
  clientSecret: xxxxxxxxxxxxx   #生成的clientSecret
  repo: rookflying.github.io    #仓库名称
  owner: rookflying    #github用户名
  admin: rookflying
  distractionFreeMode: true #是否启用类似FB的阴影遮罩
```

gitalk需要一个Github Application,[点击注册](https://github.com/settings/applications/new)

![](https://github.com/rookflying/rookflying.github.io/blob/master/img/github_jekyll/register_github_application.png?raw=true)

Homepage URL 和 Authorization callback URL 填的都是博客地址，即https://xxx.github.io。如果自己买了域名，并且解析到xxx.github.io，则也可以填域名。注册完会返回 clientId 和 clientSecret ，填入配置文件即可。

gitalk是基于 GitHub issue 开发的插件，因此需要github账户。因为是基于 GitHub issue 的，因此评论实际上就是在对应的 issue 提交 comment ，每篇文章对应一个 issue ，需要手动创建。

## 4.3 修改图标

将img下的favicon.ico替换掉即可。

# 5. 发表文章

发表的文章放在_post/目录下，文件格式是markdown，文件名格式统一为 YEAR-MONTH-DAY-NAME.md 。每个markdown文件头如下：

```
---
layout:          post
title:           快速基于GitHub Page + Jekyll搭建个人博客
subtitle:        利用现成可拉取的模版及可自定义个性化风格
date:            2018-12-16
author:          rookflying
header-img:        img/post-bg-ios9-web.jpg
catalog:         true
tags:
    - Jekyll
    - github
---
```

自行修改即可。把要发布的文章放入该目录，同步到远程master分支即可。

# 6. index.html/about.html/tags.html

index.html ， about.html ， tags.html 分别对应 HOME 主页， ABOUT 页和 TAGS 页。 ABOUT 页和 TAGS 页的背景图和文字（ description ）需要在 about.html 和 tags.html 的文件头里配置。 HOME 页的背景图在全局配置文件里配置，文字在 index.html 的文件头里配置。

# 7. 自己的域名

可以在各种云服务商购买自定义域名，如腾讯云，阿里云等，都需要进行实名认证，一般一个工作日内就认证成功。购买之后进入域名管理，点击解析：

![](https://github.com/rookflying/rookflying.github.io/blob/master/img/github_jekyll/domain_1.png?raw=true)

添加两条记录：

![](https://github.com/rookflying/rookflying.github.io/blob/master/img/github_jekyll/domain_2.png?raw=true)

CNAME类型比较好配置，记录值填的是博客原始地址，博客原始地址用的是 github 下的二级域名，不建议直接填 ip ，ip 有可能会变。填完之后查看解析状态，一般会提示你需要修改dns服务器，如果确认已修改，则忽略不用管。官方说明为使各地运营商解析同步，最长需要72小时。因此需要等待，几小时之后再回来看看。

同时需要在远程master分支上添加CNAME文件，文件内容只有一行，就是自己的域名。当域名解析状态变成“正常解析”时，就可以使用域名访问了。

# 8. SEO优化

SEO优化（搜索引擎优化）则又是一个很广的领域，简单地说就是利用搜索引擎可以搜索到自己的站点。如在搜索引擎搜索：

```
site:xxxxx.com
```

如果站点已被收录，则会显示结果。利用这个可以验证站点是否被收录。

这里介绍利用sitemap文件使站点被收录的方法。

## 8.1 sitemap

一个站点如果不做任何SEO优化，搜索引擎如百度谷歌很难发现站点的存在，也许总有一天终于被发现了，但速度太慢了。因此我们可以主动提交站点信息给搜索引擎。

sitemap（站点地图）其实就是该站点上各个网页的地址，将该文件主动提交给搜索引擎，可以提高收录效率（并不是一定会被收录。。）。前面安装的一个插件jekyll-sitemap就是用来生成sitemap文件的，push到远程master分支以后，直接访问http://域名/sitemap.xml就可以看到sitemap文件的内容。

## 8.2 谷歌收录

用谷歌搜索 site:自己的站点 ，若站点未被收录，第一条结果就是“尝试使用 Google Search Console”。

点击进去：

- 首先添加站点，一般需要验证站点所有权，验证方式就是给你一个html文件，你需要把该文件上传到远程master分支，然后进行验证。
- 接着提交站点地图，提交方式就是输入站点地图的地址。
- 等待。收录也需要时间- -。

## 8.3 百度收录

[百度搜索资源平台](https://ziyuan.baidu.com/site/index)

- 添加站点，也需要验证，验证方式也可以采用上面所说的。
- 点击链接提交，提交方式分为自动提交和手动提交。自动提交又分为主动推送，自动推送和sitemap。上面都有说明，按需选择。
- 等待。（百度收录貌似很慢很玄学- -）

还有一些技巧比如在别的站点添加自己站点的链接等。

本文介绍差不多就完了，[最后顺便求个star~](https://github.com/rookflying/rookflying.github.io)




