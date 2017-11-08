## Hexo 主题开发

#### 一、为什么要开发一个 Hexo 主题
1.1、完成自己的心愿，打造一个属于自己的网站

1.2、锻炼自己的前端开发能力，为找工作做准备


#### 二、开发前的准备
2.1、了解 Hexo 的使用及各目录结构的功能
> [Hexo 中文文档](https://hexo.io/zh-cn/docs/index.html)

2.2、借鉴他人开发经验
>[从零开始定制 Hexo 主题](https://maintao.com/2014/hexo-theme-from-scratch/)

> [Hexo 主题开发指南](https://chensd.com/2016-06/hexo-theme-guide.html)

#### 三、实战前篇

##### 3.1 使用 Hexo 创建博客目录
``` 
$ hexo init <floder>
$ cd <floder>
$ npm install // 国内用户使用 cnpm install
```

创建的目录结构
```
.
├── _config.yml     // 主配置文件
├── package.json    // 应用程序的信息
├── node_modules    // 安装的 npm 模块 
├── scaffolds       // 模版文件夹
|   |__ draft.md
|   |__ page.md
|   |__ post.md
├── source          // 资源文件夹是存放用户资源的地方
|   ├── _drafts
|   └── _posts
|      |__ hello-world.md 
└── themes          // 主题文件夹
    |__ landscape
```

* 我们的重点在 `themes` 这个主题文件夹，将开发的 `Hexo 主题` 放在这个文件夹下。
* 要使主题生效，在`主配置文件` `_config.yml` 中修改 `theme` 配置项为这个主题的名字。


##### 3.2 `Hexo 主题` 的编写
我给我的主题取名为 `brisklife`，在 `themes` 文件夹内，新建一个名为 `brisklife` 的文件夹。

我们需要在 `brisklife` 文件夹下创建一系列必需的文件夹和文件

最终 `brisklife` 文件夹下的结构大致如下：
```
|── _config.yml // 主题配置文件
├── languages // 多语言文件夹
├── layout    // 布局文件夹
│   ├── archive.ejs // 存档页模板
│   ├── category.ejs // 分类文章列表页模板
│   ├── includes // 各页面共享的模板
│   │   ├── layout.ejs // 页面布局模板，其它的页面模板都是根据它扩展来的
│   │   ├── pagination.ejs // 翻页按钮模板
│   │   └── recent-posts.ejs // 文章列表模板
│   ├── index.ejs // 首页模板
│   ├── page.ejs // 页面详情页模板
│   ├── post.ejs // 文章详情页模板
│   └── tag.ejs // 标签文章列表页模板
└── source
    ├── css
    │   └── theme.css // 主题自定义 CSS 文件
    ├── favicon.ico
    └── js
        └── theme.js // 主题 JavaScript 文件
```

#### 四、实战中篇

下面我们会一步步在 `brisklife` 文件夹下创建所需的文件或文件夹

##### 4.1 创建 `主题配置文件` `_config.yml`

4.1.1 `主配置文件` 与 `主题配置文件` 的区别：  

`主配置文件` 和 `主题配置文件` 名字都是 `_config.yml`，  但它们所在的位置不同  
`主配置文件` 位于博客根目录下，`主题配置文件` 位于我们的主题 `brisklife` 的根目录下。

4.1.2 配置方式：  

使用 `YAML语法` 来配置数据，参考 [YAML 语言教程](http://www.ruanyifeng.com/blog/2016/07/yaml.html)

在 yml 配置文件中可以配置 对象、数组、纯量（字符串、布尔值、整数、浮点数...）
``` yml
# 字符串
title: 我的博客
# 数字
per_page: 10
# 数组
languages:
 - Java
 - JavaScript
 - PHP
# 对象
social:
  Github: https://github.com
  Weibo: https://weibo.com
  Baidu: https://baidu.com
```
以上配置信息解析转换为 JavaScript 如下：
``` js
{
    title: '我的博客',
    per_page: 10,
    languages: ['Java', 'JavaScript', 'PHP'],
    social: {
        Github: 'https://github.com',
        Weibo: 'https://weibo.com',
        Baidu: 'https://baidu.com'
    }
}
```

4.1.3 读取配置文件的数据

`主配置文件` 的配置信息解析后存储在 `全局变量` `config` 中  
`主题配置文件` 的配置信息存储在 `全局变量` `theme` 中  

因此可以通过读取 `全局变量` `config` 或 `theme` 来获取对应的主或主题配置文件的数据

4.1.4 需要配置哪些数据？

`主配置文件` 使用默认生成的配置即可，里面配置项的意义可对照 [Hexo 文档--配置](https://hexo.io/zh-cn/docs/configuration.html) 
``` yml
# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: Hexo
subtitle:
description:
author: John Doe
language:
timezone:
...

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type:

```

`主题配置文件` 中的配置信息，根据自己的设计需要来决定  
比如：与主题相关的样式、额外提供的功能等
``` yml
# 颜色配置
color:
  header: indigo
  footer: indigo
  page_nav: indigo
  side_nav: indigo darken-1
  tag: pink
# 版权信息
copyright: © 2017 example.com, All rights reserved.

# Disqus评论shortname，若为空则不启用
disqus_shortname:
# 多说shortname，若为空则不启用
duoshuo_shortname:
# 网易云跟帖productKey，从通用代码中获取，若为空则不启用
yungentie_product_key:

# Google分析track id，若为空则不启用
google_analytics:
# 腾讯分析sId，若为空则不启用
tencent_analytics:
# 百度分析 id, 若为空则不启用
baidu_analytics: e8190fefba271a1ce8f1d6bf3b367f4e

```

##### 4.2 创建 `languages` 文件夹及其子文件

4.2.1 `languages` 文件夹内的文件

Hexo 支持多语言显示，`多语言配置文件`放在`主题文件夹`下的 `languages` 文件夹内，使用 `YAML` 或 `JSON` 编写

如下 `languages` 目录结构：
```
└───languages       // 语言文件夹
    ├── default.yml // 默认使用的语言配置（英文）
    ├── zh-CN.yml   // 中文
    └── zh-TW.yml   // 繁体
```
`default.yml` 内容：
``` yml
categories: Categories
search: Search
tags: Tags
tagcloud: Tag Cloud
tweets: Tweets
prev: Prev
next: Next
...
```
`zh-CN.yml` 内容：
``` yml
categories: 分类
search: 搜索
tags: 标签
tagcloud: 标签云
tweets: 推文
prev: 上一页
next: 下一页
...
```
* 根据需求，可以自己新增其他国家语言的配置文件
* 可以把 `landscape` 主题下的 `languages` 文件夹复制过来使用，根据自己的需求再做修改 

4.2.2 指定博客使用的语言

在 `主配置文件 _config.yml` 中有一个 `language` 配置项，来设定使用的语言（不指定默认使用 `default.yml`），也可以设定多个语言，`Hexo` 会根据设定使用对应的语言配置文件。

``` yml
# 设定为简体中文（zh-CN.yml）
language: zh-CN

# 或者设定多个语言（简体和繁体的切换）
language:
 - zh-CN
 - zh-TW
```

4.2.3 读取语言文件的配置数据

在模版中，使用 `__` 或 `_p` 辅助函数来读取具体的值，如：
``` yml
# zh-CN.yml
categories: 分类
search: 搜索
tags: 标签
...
archive_b: 归档：%s
...
```
``` ejs
<%= __('categories') %> // 分类

<%= _p('archive_b', '2017') %> // 归档：2017
```

##### 4.3 创建 `layout` 文件夹及其子文件

`layout` 存放主题的模版文件，决定了网站内容的呈现。  
这里选择 `EJS模版引擎` 来处理模版文件生成 html，这样在模版文件就可以使用 ejs 提供的功能。

`layout` 目录结构如下：
``` 
└───layout          // 模版文件夹
    ├── index.ejs   // 首页模版
    ├── archive.ejs // 归档页模版
    └── tag.ejs     // 标签页模版
    ...
```

之后我们主要的工作就是编写这些模版

##### 4.4 创建 `source` 文件夹及其子文件

`source`文件夹放置我们的 `css` 和 `js`等资源文件，这样我们就可以在模版文件中引用

`source` 目录结构大致如下：
``` 
└───source              // 资源文件夹
    ├── css             // css文件夹
    |   |── main.css
    |   └── index.css
    ├── js              // js文件夹
    └── img             // img文件夹
    ...
```

#### 五、实战下篇

这篇主要记录在 `layout文件夹` 下编写各模版文件的过程

##### 5.1 首页的编写

在 `layout文件夹` 下新建一个 `index.ejs` 的模版文件

5.1.1 首页要展示的内容

* 显示所有文章


