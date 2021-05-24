---
title: ML LinearModel
author: raojiyong
date: 2021-05-17 15:00:00 +0800
categories: ["2021","05"]
tags: notes
math: true
mermaid: true
---

## 多元线性回归

- $f(x)=\omega^T\omega+b$
- 决策平面：$f(x;\omega)=0$
  - 有向距离: $\gamma=\frac{f(x;\omega)}{\vert\omega\vert}$
- 最小二乘法(使均方误差最小)
  - $\hat\omega^*=arg\ min_{\hat\omega}(y-X\hat\omega)^T(y-X\hat\omega)=(X^TX)^{-1}X^Ty$
- 广义线性模型：$y=g^{-1}(\omega^Tx+b$)，其中单调可微函数 $g(\cdot)$ 称为联系函数

## 对数几率回归

- 单位跃阶函数 (Heaviside/unit-step function)：理想但不连续

$$
y=
\begin{cases}
0, &  z<0 \\
0.5, & z=0 \\
1, & z>0
\end{cases}
$$

- 对数几率函数 (logistic/Sigmoid function)
  - $g=ln\frac{y}{1-y}$
    - 几率：$\frac y{1-y}$ ，反映了 $x$ 作为正例的相对可调性
  - $g^{-1}=S(x)=\frac 1{1+e^{-x}}$
    - $S(x)'=s(x)(1-S(x))$
- 对数几率回归：用线性模型逼近真实标记的几率
  - $ln \frac{p1}{p0}=\hat x\beta=(x,1)(\omega;b)$
    - 二分类：$y_ia+(1-y_i)b=a^{y_i}b^{1-y_i}$
  - Maxmimum likelihood method
    -  $l(\beta)=\sum_{i=1}^mlmp(y_i\vert x_i;\beta_i)=\sum_{i=1}^my_iln(g(\hat x_i\beta)+(1-y_i)ln(1-g(\hat x_i\beta)))$
    -  $l'=\sum_{i=1}^m(y_i-g(\hat x\beta))\hat x_i^T=X^T(Y-g(\beta^TX))$
    -  $l''=\sum_{i=1}^m\hat x_i\hat x_i^Tp_1(x_i^T;\beta)(1-p_1(\hat x_i;\beta))$
  - 交叉熵做损失函数梯度下降
- 梯度下降: $\theta_{i+1}=\theta_i-\alpha\frac{\partial L}{\partial\theta}$

## Softmax回归

- $p(y=c\vert x)=softmax(\omega^T_cx)=\frac{exp\left(\omega_c^Tx\right)}{\sum^C_{c'=1}exp(\omega^T_{c'}x)}=\frac{exp(W^Tx)}{1_C^Texp(W^Tx)}$

## LDA

- 给定训练集数据，设法将样例投影到一条直线上，使得咏雷样例投影点尽可能接近，异类投影点尽可能远
- 协方差矩阵: $\sum=\frac 1{n-1}(X-\mu I)(X-\mu I)^T$
  - $\sum_{ij}=\sigma(x_i,x_j)$
  - 投影后: $\omega^T\sum\omega$

|                              | 两类                                                    | 一般                                          |
| ---------------------------- | ------------------------------------------------------- | --------------------------------------------- |
| within-class scatter matrix  | $S_\omega=\sum_0+\sum_1$                                | $S_m=\sum_{i=1}^N \sum_i$                     |
| Between-calss scatter matrix | $S_b=(\mu_0-\mu_1)(\mu_0-\mu_1)^T$                      | $S_b=\sum_{i=1}^Nm_i(\mu_i-\mu)(\mu_i-\mu)^T$ |
| 全局散度矩阵                 | $S_t=S_b+S_\omega$                                      | $\sum_{i=1}^m(x_i-\mu)(x_i-\mu)^T$            |
| 优化目标                     | $max_\omega\frac{\omega^TS_b\omega}{\omega^TS_w\omega}$ | $max_W\frac{tr(W^TS_bW)}{tr(W^TS_wW)}$        |
| 闭式解                       | $w=S_w^{-1}(\mu_0-\mu_1)$                               | $S_w^{-1}S_b$前$k$大广义特征向量              |



​        