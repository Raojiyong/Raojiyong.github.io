---
title: Notes on backpropagation
author: raojiyong
date: 2021-09-03 19:00:00 +0800
categories: ["2021","09"]
tags: [notes, nn]
math: true
mermaid: true
---

## Some common loss function backpropagation

### 1. SVM

**hinge loss**

$$
L_i=\sum_{j\neq y_i}\max(0,\omega_j^Tx_i-\omega_{y_i}^Tx_i+\Delta)
$$


**SVM** full loss:

$$
L=\frac1N\sum_i\sum_{j\neq y_i}[\max(0,f(x_i,W)_j-f(x_i;W)_{y_i}+\Delta)]+\lambda\sum_k\sum_lW_{k,l}^2 \\
$$


where $W_{k,l}^2$ is all square elements of $W$.

its backpropagation process is below:


$$
\begin{align}
\text{dW}_j&=\frac{X_i}{N} \\
\text{dW}_{y_i}&=\frac{-X_i}{N} \\
\text{dW}&=\text{dW}+2\lambda W
\end{align}
$$

### 2.  Cross entropy error with logistic activation

In a classification task with two classes, it is standard to use a neural network architecture with a single logistic output unit and the cross-entropy loss function. The output predication is between zero and one, and is interpreted as a probability.

We consider a network with a single hidden layer of logistic units, multiple logistic output units.

The cross entropy error:


$$
E=-\sum_{i=1}^{nclass}(t_i\log(y_i)+(1-t_i)\log(1-y_i))
$$
where $\text{t}$ is the target vector, $\text{y}$ is the output vector. Outputs are computed by applying the logistic function to the weighted sums of the hidden layer activations, $s$,
$$
y_i=\frac1{1+e^{-s_i}} \\
s_i=\sum_{j=1}h_j\omega_{ji} \\
$$


Compute the derivative of the error w.r.t each weight connecting the hidden units to the output units using chain rule.

$$
\frac{\partial E}{\partial\omega_{ji}}=\frac{\partial E}{\partial y_i}\frac{\partial y_i}{\partial s_i}\frac{\partial s_i}{\partial \omega_{ji}}
$$


Examining each factor in turn:

$$
\begin{equation}
\begin{aligned}
\frac{\partial E}{\partial y_i}&=\frac{-t_i}{y_i}+\frac{1-t_i}{1-y_i} \\
&=\frac{y_i-t_i}{y_i(1-y_i)} \\
\frac{\partial y_i}{\partial s_i}&=y_i(1-y_i) \\
\frac{\partial s_i}{\partial \omega_{ji}}&=h_j \\
\end{aligned}
\end{equation}
$$


Combining things back together:

$$
\frac{\partial E}{\partial s_i}=y_i-t_i
$$


and

$$
\frac{\partial E}{\partial \omega_{ji}}=(y_i-t_i)h_j
$$


### 3. Softmax and cross-entropy error

When a classification task has more than two classes, it is standard to use

The softmax activation of $i$-th output unit is:


$$
y_i=\frac{e^{s_i}}{\sum_{c}^{nclass}e^{s_c}}
$$


and the cross entropy error function for multi-class output is:

$$
E=-\sum_i^{nclass}t_i\log(y_i)E=-\sum_i^{nclass}t_i\log(y_i)
$$

$t$ is the target vector. Thus, computing the gradient yields:


$$
\begin{align}
\frac{\partial E}{\partial y_i}&=-\frac{t_i}{y_i} \\
\frac{\partial y_i}{\partial s_k}&=
\begin{cases}
\frac{e^{s_i}}{\sum_{c}^{nclass}e^{s_c}}-(\frac{e^{s_i}}{\sum_{c}^{nclass}e^{s_c}})^2 & i=k \\
-\frac{e^{s_i}e^{s_k}}{(\sum_{c}^{nclass}e^{s_c})^2} & i\neq k \\
\end{cases}
\\ &=\begin{cases}
y_i(1-y_i) & i=k\\
-y_iy_k & i\neq k
\end{cases}
\end{align}
$$

$$
\begin{aligned}
\frac{\partial E}{\partial s_i}&=\sum_k^{nclass}\frac{\partial E}{\partial y_k}\frac{\partial y_k}{\partial s_i} \\
&=\frac{\partial E}{\partial y_i}\frac{\partial y_i}{\partial s_i}-\sum_{k\neq i}\frac{\partial E}{\partial y_k}\frac{\partial y_k}{\partial s_i} \\
&= -t_i(1-y_i)+\sum_{k\neq i}t_ky_i \\
&= -t_i+y_i\sum_kt_k \\
&=y_i-t_i \\
\end{aligned}
$$



