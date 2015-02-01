---
layout: post
title: "Bootstrap笔记"
description: ""
category: blog
tags: [bootstrap]
---
{% include JB/setup %}

花了一个周末看完《bootstrap实战》（成林 著），因为以前有BS的经验，看的比较快。
看来看实体书还是不错，因为以前有些没搞清楚的地方在实际使用中花了大量时间在网上找解决方法，有时解决的还不好，通过系统的看一遍此书，尤其重点关注了以前思路不清晰的地方，比如data属性和javascript对BS插件的处理方式。

<!--more-->

除了BS的知识，这本书还较好的从原理上讲解了CSS设计思路、栅格系统和布局、响应式设计、LESS、JQuery设计思路等知识；在此记录下一些有用的资源和几个我关注的问题。

此书有提供了很多资源，记录一下：

- 主站：www.getbootstrap.com
- 源码：https://github.com/twbs/bootstrap/
- 中文站：www.bootcss.com   （中文文档：docs.bootcss.com）
- CDN: 全球CDN可以从www.getbootstrap.com上找到，国内的从www.bootcss.com上找到，还有www.bootstrapcdn.com
- 商业模板：wrapbootstrap.com
- 网站精选：英文：expo.getbootstrap.com，中文：expo.bootcss.com
- 插件：在中文站上有不少插件，颜色选择器，日期选择器，JQueryUI都不错
- 工具：

>https://jetstrap.com  这个收费，但是真心好用
>www.layoutit.com 这个不收费，也够用。源码还可以下载 https://github.com/justjavac/layoutit/   （从 justjavac.com 来的）
>对于响应式页面，mediaqueri.es提供了很多案例，可以参考不同大小页面的布局；Benjamin Keen的工具简直太好用了：http://www.benjaminkeen.com/open-source-projects/smaller-projects/responsive-design-bookmarklet/

- 字体图标：font awesome： http://fortawesome.github.io/Font-Awesome/
- IE6/IE7支持：采用Bsie http://ddouble.github.io/bsie
-  Metro UI: (因我不用，没有去check)，

>BootMetro: aozora.github.io/bootmetro/  
>Bootswatch: bootswatch.com/cosmo/
>Metro UI CSS: github.com/olton/Metro-UI-CSS/archive/master.zip
>MelonHTML5: codecanyon.net/item/melonhtml5-metro-ui/2986068
>Metro Mania: responsivewebinc.com/premium/metro/

最后，此书提到的 JS this 相关内容对我也很有用，在javascript中，this是一个关键字，我在使用JQuery, Bootstrap和Coffeescript组合的时候经常搞不清楚this的处理，作者在书中还是讲解的比较清楚：

1. this是关键字，不是属性；因此使用上像变量，但是不能赋值
2. this是晚绑定的，需要根据上下文判断，它可以是全局对象、当前对象或者特定对象
3. 全局代码中的this，在浏览器中表示window对象
{% highlight javascript %}
    alert(this);
{% endhighlight %}
4. 在单纯的函数定义中，也是表示全局对象window；在javascript的严格模式下（BS缺省是严格模式）是不允许的
{% highlight javascript %}
    function foo(x) {
      this.x = x;
    }
    foo(2);
    alert(x);   //2, x是全局变量
{% endhighlight %}
5. 在对象的方法定义中，this指向当前调用对象
{% highlight javascript %}
    var n = "true";
    var p = {
      n: "false",
      m: function() {
        console.log(this.n);
      }
    }
    p.m();  //结果是"false"， 而不是全局变量n的“true”
{% endhighlight %}
6. 在对象的构造函数中，this指向新创建的实例对象
{% highlight javascript %}
    function F(x) {
      this.x = x;
    }
    var f = new F(2);  // f.x 是 2
{% endhighlight %}
7. 在对象的方法定义中，使用了外层函数，则外层函数中的this指向的是全局对象
{% highlight javascript %}
    var n = "true";
    var p = {
      n: "false",
      m: function() {
        var say = function() {
            console.log(this.n);
        };
        say();
      }
    }
    p.m();  // 结果是 “true”，全局对象的值
{% endhighlight %}
处理方法是将this作为变量保存，这个变量通常用that或者self命名
{% highlight javascript %}
    var n = "true";
    var p = {
      n: "false",
      m: function() {
        var that = this;
        var say = function() {
            console.log(that.n);
        };
        say();
      }
    }
    p.m();  // 结果是 “false”，对象中的值
{% endhighlight %}
8. 使用call或者apply设置this，这时this代表制定的对象，如call函数的第一个参数
9. 在BS的JS中，this可能指的是两种对象之一，可能是一个JQuery对象，也可能是一个DOM对象，尤其是对JQuery对象调用each()方法时
{% highlight javascript %}
    $.fn.button = function (option) {
      return this.each(function () {  // 这里的this是JQuery对象
        var $this=$(this);  // 这里的this是DOM对象，通过$()方法转换为JQuery对象$this
        var data=$this.data('button');
        var options=typeof option == 'object' && option;
        if (!data) $this.data('button', (data=new Button(this, options));
        if (option == 'toggle') data.toggle();
        else if (option) data.setState(option);
      });
    }
{% endhighlight %}
