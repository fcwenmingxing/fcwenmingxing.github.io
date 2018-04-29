---
layout: post
title:  "机器学习笔记之逻辑回归(Logistic Regression)"
date:   2018-02-10 15:14:54
categories: 机器学习
tags: 机器学习 Logistic-Regression 逻辑回归
excerpt: 机器学习笔记。
mathjax: true
typora-root-url: ..
typora-copy-images-to: ..\pic\2018-04-29-Logistic-Regression
---



逻辑回归是分类当中极为常用的手段，因此，掌握其内在原理是非常必要的。

### 问题描述

假设有一个二分类问题，输出为$y∈{0,1}$, 而线性回归模型产生的预测值为$z=w^Tx+b$是实数值，我们希望有一个理想的阶跃函数来帮我们实现z值到0/1值的转化。 

![](/pic/2018-04-29-Logistic-Regression/1525011538497.png)

然而该函数不连续，我们希望有一个单调可微的函数来供我们使用，于是便找到了Sigmoid function来替代。

![1525011628555](/pic/2018-04-29-Logistic-Regression/1525011628555.png)

两者的图像如下图所示

![1525011650982](/pic/2018-04-29-Logistic-Regression/1525011650982.png)