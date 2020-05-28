---
title: hexo的使用 2
date: 2019-08-02 23:10:02
tags: hexo
---
# 标签插件

hexo中对文章输出的特定标签格式

##  quote

在文章中插入引言，可包含作者、来源和标题
代码格式

``` bash
{% blockquote [author[, source]] [link] [source_link_title] %}
content
{% endblockquote %}
```

示例

{% blockquote David Levithan, Wide Awake %}
Do not just seek happiness for yourself. Seek happiness for all. Through kindness. Through mercy.
{% endblockquote %}

##  code

在文章中插入代码。
代码格式

``` bash
{% codeblock [title] [lang:language] [url] [link text] %}
code snippet
{% endcodeblock %}
```
可以使用三对反引号包裹的格式，效果相同
示例

{% codeblock %}
alert('Hello World!');
{% endcodeblock %}


更多资料请访问[hexo](https://hexo.io/zh-cn/docs/tag-plugins)
