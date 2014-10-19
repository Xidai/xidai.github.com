---
layout: post
title: "关于KMP算法的next数组"
description: ""
category: 
tags: ["KMP", "Algorithms"]
---
{% include JB/setup %}

一把年纪了还来学KMP... 折腾一番之后写个心得笔记.

判断一个字符串是否是另一个字符串的子字符串, 可能人人都能写出一个暴力算法, 但是这种算法在解决如"aaaaaab"是否是"aaaaaaaaaaaaaaaaaaaab"的子字符串这样的问题时的复杂度会达到MN(M是子字符串的长度, N是文本的长度). KMP算法可以使得在最坏情况下的复杂度达到M+N.

KMP的核心思想就是不浪费已经匹配出来的字符串, 从而达到减小时间复杂度的目的. 一共两个步骤, 第一步, 对所要匹配的子字符串(或称为pattern)进行预处理, 得到一个长度为pattern字符串长度的数组(可称为next数组, partial match table等等), 第二步, 运用第一步中求出来的数组匹配字符串, 如果找到匹配的, 返回子字符串在文本(或称为text)中的起始下标, 如果没找到, 则返回-1.

关于在第二步中如何运用next数组来进行匹配的,这里有篇文章说得很详细, 手把手教的...[The Knuth-Morris-Pratt Algorithm in my own words](http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/). 真正难的是在第一步. 网上的文章实现方法都差不多, 但是关于怎么理解这段代码基本上每个人都有适合自己思维方式的解释. 这里说说我是怎么理解的.

<!--more-->