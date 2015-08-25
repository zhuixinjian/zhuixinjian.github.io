---
layout: post
title: Checkbox on github pages
category: jekyll
tags: ['Checkbox','Jekyll','redcarpet','Font-Awesome']
published: True
comments: True

---

想做一个Task list清单,但Jekyll自带的`markdown: redcarpet`不支持Checkbox

翻看网上各种办法.其实[(issues)][1]中的解决办法很好,但是没被[redcarpet][2]的开发者收录,
那就从`content`的输出结果中去replace `<li>[ ]`和`<li>[x]`

{% highlight ruby %}
{% raw %}
{{ content | replace: '<li>[ ]', '<li class="check-none">' | replace: '<li>[x]', '<li class="check-done">'}}
{% endraw %}
{% endhighlight %}

我套用[Font-Awesome][3]的样式做出了一个还不错的TaskList:

<!--more-->

{% highlight ruby %}
{% raw %}
{{ content | replace: '<li>[ ]', '<li><i class="fa fa-square-o"></i>' | replace: '<li>[]', '<li><i class="fa fa-square-o"></i>' | replace: '<li>[x]', '<li><i class="fa fa-check-square-o"></i>' | replace: '<li>[X]', '<li><i class="fa fa-check-square-o"></i>'  }}
{% endraw %}
{% endhighlight %}


<i class="fa fa-square-o"></i> `<i class="fa fa-square-o"></i>`
<i class="fa fa-check-square-o"></i> `<i class="fa fa-check-square-o"></i>`


###Example:
- [x] done 
- [x] plan 1
	- [x] plan 2 done
	- [ ] plan 3
	- [x] plan 4 done
- [] Plan 5
- [X] Plan 6 done
- [ ] this is still to do


[1]: https://github.com/vmg/redcarpet/issues/323
[2]: https://github.com/vmg/redcarpet
[3]: https://fortawesome.github.io/Font-Awesome/