---
layout: post
title: HOW TO USE TAGS AND CATEGORIES ON GITHUB PAGES WITHOUT PLUGINS
category: 'tech_web'
tags: ['Jekyll','Github Pages']
published: True
comments: True
shares: True
---

[Github Pages][2] 很帅,[Jekyll][3]这个基于`MarkDown`的博客系统也很帅 :smile:
, 不过还是有很多限制的:

- [支撑少量的插件][1]
- 不允许自定义插件

所以没有`Tag`,`Category`等功能.

一个博客系统没有`Tag`,`Category`怎么活?

于是乎开始折腾,翻看[Jekyll API][3],研究[Liquid][4]语法,给这个博客搭建了一个`Tag`,`Category`界面,记录一下,帮助以后扩展其他页面.

<!--more-->

### 准备事项
- [Jekyll API][3]
- [Liquid][4]语法
- [Github Pages][2]
- [参考网站][5]

### 走过的坑
- Github Pages 是一个静态站点,所以不支持任何传参 :broken_heart:
- 不支持传参数,那就想办法截取`url`,结果绕不过`permalink` :broken_heart:
- 网上各种例子都必须维护一套巨大的`Category`,`Tag`库. 写个博客还不够累的. :broken_heart:

好在[Jekyll][3]提供了一个`site.tags.TAG`,`site.categories.CATEGORY` [Link][6] 的方法,
> The list of all Posts with tag TAG.

### Do it
于是创建了如下这个界面,把所有的帖子按照`Tag`来进行分组显示

`tag.html`

{% highlight html %}
{% raw %}
---
layout: default
title: Tags
permalink: /blog/tags/
---

<header class="post-header">
	<h1>Tags</h1>
</header>

<section id="archive">
    {% for post_info in site.tags %}
    	{% assign post_tag = post_info[0] %}
    	{% assign tag = site.data.tags[post_tag] %}
    	{% if tag == null %}
    		{% assign tag = post_tag %}
    	{% endif %}
	<h2 class="ahour"><a name="{{post_tag}}">{{ tag }} ({{ post_info[1].size }}):</a></h2>
	<ul>
		{% for post in post_info[1] %}
		<li style="list-style-type:none;"><time>{{ post.date | date: "%m-%d" }}</time><a href="{{ post.url }}">{{ post.title }}</a></li>
		{% endfor %}
	</ul>
    {% endfor %}
</section>
{% endraw %}
{% endhighlight %}

这个中间有一个小技巧后面会用到,那就是给每个标签打一个锚点

```html
<h2 class="ahour"><a name="{{post_tag}}">{{ tag }} ({{ post_info[1].size }}):</a></h2>
```

### Post.html添加标签

{% highlight html %}
{% raw %}
<article class="post-content">
  {{ content }}

  {% assign category = site.data.categories[page.category] %}
  <p id="post-meta">Posted 
  {% if category == null %}
    {% assign category = page.category %}
  {% endif %}
  in <code><a href="/blog/category/#{{ page.category }}">{{ category }}</a></code>
  

  {% assign tag_size = page.tags.size %}
  {% if tag_size > 0 %}
    with tag:<i class="fa fa-tags"></i>
    {% for post_tag in page.tags %}
        <a href="/blog/tags/#{{post_tag}}">{{ post_tag }}</a>{% if forloop.last == false %},{% endif %}
    {% endfor %}
  {% endif %}</p>
</article>
{% endraw %}
{% endhighlight %}

核心就是用上面的锚点来跳转,也算是实现了`Tag`和`Category`

{% highlight html %}
{% raw %}
<a href="/blog/tags/#{{post_tag}}">{{post_tag}}</a>
{% endraw %}
{% endhighlight %}

### 预览效果

- [Tag预览页][7]
- [Category预览页][8]


[1]: https://pages.github.com/versions/
[2]: https://pages.github.com
[3]: http://Jekyllrb.com
[4]: https://github.com/Shopify/liquid/wiki/Liquid-for-Designers
[5]: http://www.minddust.com/post/tags-and-categories-on-github-pages/
[6]: http://jekyllrb.com/docs/variables/#site-variables
[7]: {{site.url}}/blog/tags/
[8]: {{site.url}}/blog/categories/