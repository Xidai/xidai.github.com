---
layout: post
title: "JavaScript中的Date对象"
description: ""
category: 
tags: []
---
{% include JB/setup %}

一直都不太会用Date对象, 基本靠蒙... 最近好好查了一些资料, 总结一下.

有几点最基本的要记住: 

1. 给定一个时间, 如果不给时区信息, 那这个时间是没有意义的.
2. 任何一个Date对象都是带有时区信息的. 我们不手动给它指定时区, 不代表JavaScript不给它指定.
3. 提到[UTC时间](http://en.wikipedia.org/wiki/Coordinated_Universal_Time)或[GMT时间](http://en.wikipedia.org/wiki/Greenwich_Mean_Time)的时候, 理解为0时区时间就好.

####1. 构造函数####

Date有四个构造函数, 分别接受0个参数, 一个表示毫秒数的number类型的参数, 一个string类型的参数, 至少2个最多7个分别表示年月日时分秒以及毫秒的number类型的参数. 而实际上也可以理解为只有前两种, 因为后两种会分别调用`Date.parse()`和`Date.UTC()`, 而这两个方法都会返回毫秒数. 

<!--more-->

<script src="https://gist.github.com/Xidai/7902d6bf44256f7d76d3.js"></script>


这里面比较容易感到confuse的是`Date(dateString)`这个构造函数, 到底`dateString`的格式可以是怎样的? 这里的`dateString`可以是符合[IETF-compliant RFC 2822 timestamps](http://tools.ietf.org/html/rfc2822#page-14)和[ISO8601](http://www.ecma-international.org/ecma-262/5.1/#sec-15.9.1.15)的.


####2. 方法####

对于getter和setter方法, 基本都有两个版本, 一个是用于get/set UTC时间的, 一个是用于本地时间的.