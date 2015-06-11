---
layout: post
title: "CoffeeScript笔记"
description: ""
category: blog
tags: [coffeescript, javascript]
---
{% include JB/setup %}

边看边记《CoffeeScript程序设计》（Mark Bates 著, Goddy Zhao 译）。
之前已经在用CoffeeScript，主要是直接从[CoffeeScript](http://www.coffeescript.org/)开始。
这次希望快速系统的梳理一遍，在此记录下我所关注的要点和容易忽视的细节。

<!--more-->

- CoffeeScript的主站：[www.coffeescript.org](http://www.coffeescript.org)
- 此书源码：[github.com/markbates](https://github.com/markbates/Programming-In-CoffeeScript)
- 参考信息：

>主站通过一页简洁明快的总结了CoffeeScript的语法，非常有用。在此仅记录阅读此书和相关资源的过程中，
>在主站上没有列出的用于信息

### Range
注入数值：将一个数组插入到另一个数组中，从第n个位置开始，原数组中的项依次后移，注意-1的使用

{% highlight coffeescript %}
    arrayA = [1..10]
    arrayA[4..-1] = ['a', 'b', 'c', 'd']
    console.log arrayA
{% endhighlight %}

结果是：
>[1,2,3,4,'a','b','c','d',5,6,7,8,9,10]

### Loop
在对键值对对象进行的for循环中，是对对象的所有属性进行循环处理，这是如果对象通过prototype函数设置的属性也会加入循环。
如果只关心局部定义的属性键值对，则需要加own关键字

{% highlight coffeescript %}
    objectA =
      prop_1: "1"
      prop_2: "2"

    for key, value of objectA
      console.log "#{key}: #{value}"

    Object.prototype.prop_3 = "3"

    for key, value of objectA
      console.log "#{key}: #{value}"

    for own key, value of objectA
      console.log "#{key}: #{value}"
{% endhighlight %}

第一个for的结果是：
>prop1: 1
>prop2: 2

第二个for的结果是：
>prop1: 1
>prop2: 2
>prop3: 3

第三个for的结果是：
>prop1: 1
>prop2: 2

### Do语句
用do来分割作用域，提供是用到timeout函数时，以避免JavaScript的异步特性。

{% highlight coffeescript %}
  for x in [1..5]
    do (x) ->
      setTimeout ->
        console.log x
      , 1
{% endhighlight %}

### Class
当类的构造函数需要多个参数时，较好的constructor函数定义是：

{% highlight coffeescript %}
  class Person
    constructor: (options) ->
      {@name, @age, @height} = options
{% endhighlight %}

或者

{% highlight coffeescript %}
class Person
  constructor: (attributes) ->

  print: ->
    console.log "name: #{@attributes.name}"
{% endhighlight %}

#### 类函数（静态函数）和类属性（静态属性）
通过在函数名前面添加@，可以定义类函数；
通过在变量名前面添加@，可以定义类属性；（没见到示例，等等测下）

{% highlight coffeescript %}
class Person
  constructor: (attributes) ->

  @printUsage: ->
    console.log "person = new Person(name, age)"
{% endhighlight %}

#### 修改对象原型（Object.prototype）的方法是::
{% highlight coffeescript %}
String::dasherize = ->
  this.replace /_/g, "-"
{% endhighlight %}
