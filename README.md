# Rookflying's blog

[![](https://travis-ci.org/rookflying/rookflying.github.io.svg?branch=master)](https://travis-ci.org/rookflying/rookflying.github.io)
[![](https://img.shields.io/github/release/rookflying/rookflying.github.io.svg)](https://github.com/rookflying/rookflying.github.io/releases)
![](https://img.shields.io/badge/ruby-v2.4.1-blue.svg)
![](https://img.shields.io/badge/jekyll-v3.8.5-blue.svg)

## [view blog](https://rookflying.com/)
## [中文教程](https://rookflying.com/2018/12/16/%E5%BF%AB%E9%80%9F%E5%9F%BA%E4%BA%8EGitHub-Page-+-Jekyll%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)

## Introduction

This repo is forked from [Huxpro](https://github.com/Huxpro/huxpro.github.io) and [qiubaiying](https://github.com/qiubaiying/qiubaiying.github.io). Thanks to them.

GitHub generate the site according to the master branch. Make sure that the updated content is merged to the master or directly push to the master.

## Environment

### Mac or Linux

- install rvm

```
curl -L https://get.rvm.io | bash -s stable
```

- install ruby

```
rvm use 2.4.1
```

If you don't have the specified version of ruby, you will be prompted to install it.

- install jekyll and jekyll-paginate

```
gem install jekyll
gem install jekyll-paginate
```

## Get Started

After you clone this repo, run `jekyll serve` in Command Line and preview them themes in your browser. The default port is 4000, so the url will be `http://127.0.0.1:4000/`.

## Configuration

The entire project is configured through this file `_config.yml`. Actually, only need to focus on this file.

### Personal Information

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

Modify personal information and can view the result in local environment.

### Sidebar

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

The `SNS settings` is about some links to other platforms. You can add some content by yourself.

For example:

```
platform_username:     username
```

Also need to add some code shown below to `_layouts/page.html` and `_includes/footer.html` in the right place.

```
{% if site.platform_username %}
        <li>
                <a target="_blank" href="https://www.platform.com/people/{{ site.platform_username }}">
                      <span class="fa-stack fa-lg">
                           <i class="fa fa-circle fa-stack-2x"></i>
                           <i class="fa  fa-stack-1x fa-inverse">platform_name</i>
                      </span>
                </a>
       </li>
{% endif %}
```

### Gitalk Plugin

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


Gitalk needs a Github Application. [register](https://github.com/settings/applications/new)

After registration, it will return clientId and clientSecret. Fill them in the configuration file. Because it is based on the GitHub issue, the comment is actually a comment submitted in the corresponding issue. Each article corresponds to an issue which needs to be created manually.

### Edit icon

Replace /img/favicon.ico.

### Post an Article

Posted articles are placed in the `_posts/`. File format is markdown and filename format is unified to `YEAR-MONTH-DAY-NAME.md`. The header of each markdown file is as follows:

```
---
layout:          post
title:           title
subtitle:        subtitle
date:            2018-12-16
author:          rookflying
header-img:        img/image.jpg
catalog:         true
tags:
    - Jekyll
    - github
---
```

### Tag Configuration

```
# Featured Tags
featured-tags: true                     # 是否使用首页标签
featured-condition-size: 0              # 相同标签数量大于这个数，才会出现在首页
```

## License

See the [LICENSE](https://github.com/rookflying/rookflying.github.io/blob/master/LICENSE) file.


 








