---
layout: post
title: "一个寻找最大素因子的算法"
description: ""
category: 
tags: ["Project Euler", "Algorithms"]
---
{% include JB/setup %}

被[Project Euler](http://projecteuler.net/problems)的第三题卡住了...题目如下:

>The prime factors of 13195 are 5, 7, 13 and 29.
>What is the largest prime factor of the number 600851475143 ?

我的brute force的代码就不贴了, 反正跑不出结果... 在网上搜到一个答案并提交后, 进到这道题的讨论区里, 发现@bitRAKE的一个非常简短的代码(原代码是C, 我改为了python):

<!--more-->
<script src="https://gist.github.com/Xidai/a3f423126d85b3fa3fcf.js"></script>

第一反应就是竟然不用判断是否素数?! 一番思考后, 才理清了这里面的原理.

任意一个大于1的正整数N都能写成<code>N = P<sub>1</sub> * P<sub>2</sub> * ... * P<sub>i</sub></code>. 其中<code>P<sub>1</sub></code>到<code>P<sub>i</sub></code>为从小到大排列的素数, 相邻的两个数可能相等(如`4 = 2 * 2`). 于是<code>P<sub>i</sub></code>就是我们要找的最大素因子.

显然, 要找到<code>P<sub>i</sub></code>, 只需计算<code>N / (P<sub>1</sub> * P<sub>2</sub> * ... * P<sub>i - 1</sub>)</code>就可以了, 以此类推, 需要依次找到<code>P<sub>1</sub></code>, <code>P<sub>2</sub></code>..., 废话...

于是首先我们可以计算出<code>n<sub>1</sub> = N / P<sub>1</sub></code>, 然后是<code>n<sub>2</sub> = n<sub>1</sub> / P<sub>2</sub></code>, 直到<code>n<sub>i</sub> = n<sub>i-1</sub> / P<sub>i</sub></code>, 此时<code>n<sub>i</sub></code>等于1, 于是除数就是答案了. 至此, 循环的终止条件就被确定下来了, 即<code>n = 1</code>. (实际上把这个终止条件找对就已经成功了, 即使在代码中依然有判断素数的逻辑, 结果也是瞬间就出来.)

接下来就是找到那一系列素数了. 从2开始依次去除`n`, 第一个使得余数为0的除数就是一个`P`. 这就是@bitRAKE的代码的逻辑. 为什么不用判断这个除数是否是素数? 很简单, 因为它一定是素数... 用反证法就可证明. 假设第一个使得余数为0的除数是一个合数`C`, 那么它一定可以写成`C = M * N`, `M`和`N`是两个小于`C`的正整数, 而`n`既然可以被`C`整除, 那就一定可以被`M`或`N`整除, 而`M`和`N`都是小于`C`的, 于是`C`一定不是第一个使得余数为0的除数. 因此第一个使得余数为0的除数一定是一个素数. 因此我们根本不用判定是否是素数!

写完以后发现原来这么简单...