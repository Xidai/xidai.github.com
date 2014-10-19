---
layout: post
title: "关于KMP算法的next数组"
description: ""
category: 
tags: ["KMP", "Algorithms"]
---
{% include JB/setup %}

判断一个字符串是否是另一个字符串的子字符串, 可能人人都能写出一个暴力算法, 但是这种算法在解决如"aaaaaab"是否是"aaaaaaaaaaaaaaaaaaaab"的子字符串这样的问题时的复杂度会达到MN(M是子字符串的长度, N是文本的长度). KMP算法可以使得在最坏情况下的复杂度达到M+N.

KMP的核心思想就是不浪费已经匹配出来的字符串, 从而达到减小时间复杂度的目的. 一共两个步骤, 第一步, 对所要匹配的子字符串(或称为pattern)进行预处理, 得到一个长度为pattern字符串长度的数组(可称为next数组, partial match table等等), 第二步, 运用第一步中求出来的数组匹配字符串, 如果找到匹配的, 返回子字符串在文本(或称为text)中的起始下标, 如果没找到, 则返回-1.

关于在第二步中如何运用next数组来进行匹配的,这里有篇文章说得很详细, 手把手教的...[The Knuth-Morris-Pratt Algorithm in my own words](http://jakeboxer.com/blog/2009/12/13/the-knuth-morris-pratt-algorithm-in-my-own-words/). 真正难的是在第一步. 网上的文章实现方法都差不多, 但是关于怎么理解这段代码基本上每个人都有适合自己思维方式的解释. 这里说说我是怎么理解的.

<!--more-->

对于pattern`ababac`, 假如说我们已经算出了next数组的前四个值, 此时`next=[0, 0, 1, 2]`, 接下来计算`next[4]`. 下图表示当前的情况.

![01](/images/2014-10-19-kmp-next-array-01.png)

对于`next[n]`来说, 在`next[n - 1]`已知的情况下, 最大的值是`next[n - 1] + 1`, 于是在这个例子中, 我们只需要看第二个字符是否等于第四个字符, 如果相等, `next[4]`就直接可以等于`next[3] + 1`了. 这里它们是相等的, 于是`next[4] = 3`. 

接下来计算`next[5]`. 下图表示当前情况.

![02](/images/2014-10-19-kmp-next-array-02.png)

同理, 现在需要比较第三位和第五位是否相等, 很遗憾这次不等了, 也就是说`next[5]`不能等于理论上的最大值`4`了, 于是我们会想到验证能不能等于3, 如果3也不行, 再看等于2行不行, 以此类推. 但这个方法看起来效率是不高的, 能不能找到一些规律让我们直接跳过某些值呢? 我们试着把上面的图变换一下, 注意把suffix部分放在prefix的上面一行, 如下:

![03](/images/2014-10-19-kmp-next-array-03.png)

是不是很眼熟了? 接下来只需要愉快地移动`j`指针就可以了! enjoy!