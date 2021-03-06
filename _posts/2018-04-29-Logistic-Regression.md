---
layout: post
title:  "机器学习笔记之逻辑回归(Logistic Regression)"
date:   2018-04-29 15:14:54
categories: 机器学习
tags: 机器学习 Logistic-Regression 逻辑回归
excerpt: 机器学习笔记。
mathjax: true
typora-root-url: ..
typora-copy-images-to: ..\inner_ref\2018-04-29-Logistic-Regression
---

* content
{:toc}

知识点

> 1. 什么是$Sigmoid function$函数，为何用$Sigmoid function$函数
> 2. 为何损失函数用交叉熵（对数损失）
> 3. 梯度推导
> 4. 延伸：梯度下降方式。。。。

* content
{:toc}



逻辑回归是分类当中极为常用的手段，因此，掌握其内在原理是非常必要的。

### 问题描述

假设有一个二分类问题，输出为$y∈{0,1}​$, 而线性回归模型产生的预测值为$z=w^Tx+b​$是实数值，我们希望有一个理想的阶跃函数来帮我们实现z值到0/1值的转化。 

![x](/inner_ref/2018-04-29-Logistic-Regression/1525011538497.png)

然而该函数不连续，我们希望有一个单调可微的函数来供我们使用，于是便找到了$Sigmoid function$来替代。

![1525011628555](/inner_ref/2018-04-29-Logistic-Regression/1525011628555.png)

两者的图像如下图所示

![1525011650982](/inner_ref/2018-04-29-Logistic-Regression/1525011650982.png)

### 代价函数定义

好了，所要用的几个函数我们都好了，接下来要做的就是根据给定的训练集，把参数w给求出来了。要找参数$w$，首先就是得把代价函数（cost function）给定义出来，也就是目标函数。 我们第一个想到的自然是模仿线性回归的做法，利用误差平方和来当代价函数。

![1525012311068](/inner_ref/2018-04-29-Logistic-Regression/1525012311068.png)

其中，$z^(i)=w^Tx^{(i)}+b$，$i$表示第$i$个样本点，$y^{(i)}$表示第i个样本的真实值，$ϕ(z^{(i)})$表示第$i$个样本的预测值。 
这时，如果我们将$ϕ^{z(i)}=1/(1+e^{−z^{(i)}})$代入的话，会发现这时一个非凸函数，这就意味着代价函数有着许多的局部最小值，这不利于我们的求解。 

![1525012552185](/inner_ref/2018-04-29-Logistic-Regression/1525012552185.png)

那么我们不妨来换一个思路解决这个问题。前面，我们提到了$ϕ(z)$可以视为类1的后验估计，所以我们有 

![1525012602474](/inner_ref/2018-04-29-Logistic-Regression/1525012602474.png)

其中，$p(y=1|x;w)$表示给定$w$，那么$x$点$y=1$的概率大小。

**上面两式可以写成一般形式** 

 $p(y|x;w)=\phi(z)^{y}(1 - \phi(z))^{(1-y)}$

 接下来我们就要用极大似然估计来根据给定的训练集估计出参数w。  $L(w)=\prod_{i=1}^{n}p(y^{(i)}|x^{(i)};w)=\prod_{i=1}^{n}(\phi(z^{(i)}))^{y^{(i)}}(1-\phi(z^{(i)}))^{1-y^{(i)}}$

**为了乘积运算在计算机中会发生溢出，我们对上面这个等式的两边都取一个对数**  

$l(w)=lnL(w)=\sum_{i = 1}^n y^{(i)}ln(\phi(z^{(i)})) + (1 - y^{(i)})ln(1-\phi(z^{(i)}))$

我们现在要求的是使得$l(w)$最大的$w$。没错，我们的代价函数出现了，我们在$l(w)$前面加个负号不就变成就最小了吗？不就变成我们代价函数了吗？ 

$ J(w)=-l(w)=-\sum_{i = 1}^n y^{(i)}ln(\phi(z^{(i)})) + (1 - y^{(i)})ln(1-\phi(z^{(i)})) $

为了更好地理解这个代价函数，我们不妨拿一个例子的来看看

$J(\phi(z),y;w)=-yln(\phi(z))-(1-y)ln(1-\phi(z))$

也就是说

$ J(\phi(z),y;w)=\begin{cases} -ln(\phi(z)) & if \ y=1 \\ -ln(1-\phi(z)) & if \ y=0 \end{cases} $

### 参考内容

[1]: https://blog.csdn.net/zjuPeco/article/details/77165974