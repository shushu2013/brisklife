## brisklife 主题

brisklife 是一款简洁的响应式 Hexo 主题，使用时确保你的 Hexo 升级到版本3以上

![brisklife](http://oet93w0rc.bkt.clouddn.com/image/github/brisklife.png)

#### 预览

[Hexo 博客](http://shushu2013.github.io/)

#### 安装
``` shell
$ cd yourblog/themes    // 切换到你的博客文件夹下的 themes 目录

$ git clone git@github.com:shushu2013/brisklife.git // 下载 brisklife 

```

#### 使用
1、brisklife 主题使用了 Hexo 3.0 新增的 [[数据文件]](https://hexo.io/zh-cn/docs/data-files.html) 功能及额外的 layout 文件，因此需要复制以下文件到你的博客目录中
> 1.1 复制 brisklife/_data 文件夹到 yourblog/source 文件夹下  
> 1.2 复制 brisklife/_md 文件夹下的所有文件夹到 yourblog/source 文件夹下

2、在 yourblog/_config.yml 主配置文件中修改 `theme` 的值为 `brisklife` 来启用主题

#### 配置
1、about (关于) 页面配置在 _data/about.json 中
``` json
    "contract": {
        "bilibili":"https://space.bilibili.com/10411908",
        "weibo": "https://weibo.com/2495087303",
        "github": "https://github.com/shushu2013"
    },
    "skills": {
        "javascript": 7,
        "html5": 8,
        "css3": 7,
        "java": 6
    }
```
>1.1 其中 `bilibili`、`weibo`、`javascript` 对应的svg图标文件在
`brisklife/source/icon` 文件夹下。  
>1.2 图标对应规则为：name.svg，比如 `weibo` 对应的图标为 `weibo.svg`。  
>1.3 如果没有，需要自己到 [iconfont](http://www.iconfont.cn)下载，并将相应图标放到 `brisklife/source/icon` 文件夹下。

2、hobby (兴趣) 页面配置在 _data/hobby.json 中

``` json
    {
        "id": "art",
        "data": [
            {
                "name": "廖墨军素描入门",
                "url": "https://www.bilibili.com/video/av4144372",
                "imgUrl": ""
            },
            {
                "name": "贵哥素描人门",
                "url": "https://www.bilibili.com/video/av7492861",
                "imgUrl": ""
            }
        ]
    }
```
> 2.1、格式：`id` 为兴趣名，`data` 下为一些链接数据。  
> 2.2、如需更改或添加兴趣名，需要在 `brisklife/languages` 下的语言配置文件中添加对应的预设语言。
``` yml
# brisklife/languages/zh-CN.yml
hobby:
  art: 艺术       # 对应 _data/hobby.json 中的 art
  history: 历史
  reading: 阅读
```