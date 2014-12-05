---
layout: post
title:  "Jekyll snippets"
date:   2014-12-02 00:05:00
categories: public
---

### Syntax highlight
{% raw %}
    {% highlight bash %}
    CODE
    {% endhighlight %}
{% endraw %}

### Raw code block
    {% raw %}
    RAW
    {% endraw %}

### Link to a post asset
{% highlight bash %}
    [Link text]({{ '/post-assets/someasset' | prepend: site.baseurl }})
{% endhighlight %}