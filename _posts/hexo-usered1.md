---
title: hexo的使用 1
date: 2019-08-02 21:04:41
tags: hexo
---
## 创建博文

通过hexo命令：

``` bash
hexo new [layout] <filename>
```

以此生成文件，再编写文件来编辑一篇博文

## 生成静态文件

通过hexo命令：

``` bash
hexo generate
```

来生成静态文件
上传至git前需要生成静态文件，git上的是hexo生成好的静态文件
该命令可以简写为

``` bash
hexo g
```

最好在使用命令前执行以下命令来去除之前的缓存

```
hexo clean
```

可以通过加上 -d 参数来同时实现部署功能

## 部署网站

hexo命令可以一键部署网站

``` bash
hexo deploy
```

更多资料请访问[hexo](https://hexo.io/zh-cn/docs/commands)
