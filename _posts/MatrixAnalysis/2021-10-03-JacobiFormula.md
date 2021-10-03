---
title: Proof of jacobi formula
author: raojiyong
date: 2021-10-03 15:00:00 +0800
categories: ["2021","10"]
tags: [matrix theory]
math: true
mermaid: true
---

## Jacobi's formula

$d\det(A)=\text{tr}(\text{adj}(A)dA)$

### Derivation

#### Via Matrix Computation

**Lemma**. Let A and B be square matrices of the same dimension *n*.

$\sum_i\sum_jA_{ij}B_{ij}=\text{tr}(A^TB)$

*Proof*: The product of *AB* of the pair of matrices has components

$(AB)_{jk}=\sum_iA_{ji}B_{ik}$  

$tr(A^TB)=\sum_j(A^TB)_{jj}=\sum_j\sum_iA_{ij}B_{ij}=\sum_i\sum_jA_{ij}B_{ij}$

**Theorem**. $d\det(A)=\text{tr}(\text{adj}(A)dA)$

*Proof:* [Laplace's formula](https://en.wikipedia.org/wiki/Laplace_expansion) for the matrix *A* can be state as 

也就是行列式通过代数余子式展开，$\det(A)=\sum_ja_{ij}c_{ij},其中c_{ij}是代数余子式,(\text{adj}A)^T_{ij}=c_{ij}$

$\det(A)=\sum_jA_{ij}\text{adj}^T(A)_{ij}$.

Notice that the summation over some arbitrary row *i* of the matrix.

The determinant of *A* can be a function of the element of *A*:

$\det(A)=F(A_{11},A_{12},\dots,A_{21}，A_{22},\dots,A_{nn})$

so that, by the chain rule, its differential is

$d\det(A)=\sum_i\sum_j\frac{\partial F}{\partial A_{ij}}dA_{ij}$

This summation is performed over all *n$\times$n* elements of the matrix.

利用 Laplace formula 带入

$\frac{\partial\det(A)}{\partial A_{ij}}=\frac{\partial\sum_kA_{ik}\text{adj}^T(A_{ik})}{\partial A_{ij}}=\sum_k\frac{\partial A_{ik}\text{adj}^T(A_{ik})}{\partial A_{ij}}$

Thus, by the product rule 求导，拆开

$\frac{\partial\det(A)}{\partial A_{ij}}=\sum_k\frac{\partial A_{ik}}{\partial A_{ij}}\text{adj}^T(A)_{ik}+\sum_kA_{ik}\frac{\partial\text{adj}^T(A)_{ik}}{\partial A_{ij}}$

在同一行/列的代数余子式对应的元素导数值为零 Thus,

$\frac{\partial\text{adj}^T(A)_{ik}}{\partial A_{ij}}=0$

so

$\frac{\partial\det(A)}{\partial A_{ij}}=\sum_k\frac{\partial A_{ik}}{\partial A_{ij}}\text{adj}^T(A)_{ik}$

All the elements of *A* are independent of each other. i.e.
$$
\begin{align}
&\frac{\partial A_{ik}}{\partial A_{ij}}=\delta_{jk}\\&\delta_{ij}=
\begin{cases}
1& \text{if}\ i= j,\\
0& \text{if}\ i\neq j.
\end{cases}
\end{align}
$$
where $\delta$ is the [Kronecker delta](https://en.wikipedia.org/wiki/Kronecker_delta), so

$\frac{\partial\det(A)}{\partial A_{ij}}=\sum_k\text{adj}^T(A)_{ik}\delta_{jk}=\text{adj}^T(A)_{ij}$

Therefore,

$d(\det(A))=\sum_i\sum_j\text{adj}^T(A)_{ij}dA_{ij}=\text{tr}(\text{adj}(A)dA).$

#### Via Chain Rule

略