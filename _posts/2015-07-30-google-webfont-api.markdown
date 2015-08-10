---
layout: post
title: "Google webfont api"
category: 'tech_web'
tags: ['WebFont','Jekyll']
comments: True
shares: True
css: <link rel="stylesheet" type="text/css" href="http://fonts.googleapis.com/css?family=Tangerine">

style: |
 <style>
 .font-css-test {
  font-family: 'Tangerine', serif;
  font-size: 48px;
  text-shadow: 4px 4px 4px #aaa;
 }
 </style>

---

### Web Font Test
我擦,业务从2C转向2B之后,需要研究下web font怎么运作的.翻看了下[Google Font Quick Start][1],核心的代码如下

1. Link font style

	```html
	<link rel="stylesheet" type="text/css" href="http://fonts.googleapis.com/css?family=Tangerine">
	```

2. Custom css selector

	```css
	.font-css-test {
	  font-family: 'Tangerine', serif;
	  font-size: 48px;
	  text-shadow: 4px 4px 4px #aaa;
	 }
	```

3. Use css style.

	```html
	<div class="font-css-test">css style just load in detail pages. so you need click in it.</div>
	```

<!--more-->

## Preview
<div class="font-css-test">
"Everything around you that you call life was made up by people, & you can change it." 
<p>via Steve Jobs </p>
</div>

The index page not load font style. plz [click][3] to preview.


## Others
恰巧也研究了下[Jekyll][2]如何在子界面定义自己的样式.主要是用到了`page`页头部的`yaml`定义, 定义了两部分内容
css & style.

```yaml
css: <link rel="stylesheet" type="text/css" href="http://fonts.googleapis.com/css?family=Tangerine">

style: |
 <style>
 .font-css-test {
  font-family: 'Tangerine', serif;
  font-size: 48px;
  text-shadow: 4px 4px 4px #aaa;
 }
 </style>
```

在`head.html`中添加如下两行代码,把子page页面中的自定义内容引用到head上

{% gist zhuixinjian/7747aab59d9b8183fee7 %}

bwt: Jekyll 没法高亮自身的一些方法和属性.就只能贴到gist再引入过来.


[1]: https://developers.google.com/fonts/docs/getting_started?csw=1#Quick_Start
[2]: http://jekyllrb.com/
[3]: {{ page.url }}