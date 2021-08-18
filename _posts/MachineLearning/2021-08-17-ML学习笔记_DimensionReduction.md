---
title: ML Dimension Reduction
author: raojiyong
date: 2021-08-17 15:00:00 +0800
categories: ["2021","08"]
tags: [notes,Machine Learning]
math: true
mermaid: true
---

## 线性降维

- 维数灾难 curse of dimensionality
  - 高维空间样本稀疏
  - 计算内积难

### MDS

Multiple Dimensional Scaling, 多维放缩

- 样本间距离在低维空间保持
- 算法
  1. 由距离矩阵 $D$ 求内积矩阵: $b_{ij}=-\frac12(D_{ij}^2-D_{i\ast}^2-D_{\ast j}^2+D_{\ast\ast}^2)$
  2. 特征值分解:$B=V\Lambda V^T$, 非零特征值构成 $\Lambda_\ast=diag\lambda_1,\lambda_2,\cdots,\lambda_d^\ast$
  3. 坐标$Z=\Lambda_\ast^{\frac12}V_\ast^T$, 可提前 $d$ 个最大特征值

### PCA (Principal Component Analysis)

- 最近重构性：样本点到这个超平面距离足够近
- 最大可分性：样本点在这个超平面上的投影尽可能的分开

$$
\begin{equation}
\begin{aligned}
\max\mathrm{tr}(W^TX&X^TW) \\
s.t. \ W^TW& =1 \\
\end{aligned}
\end{equation}
$$

- 算法

  1. 中心化
  2. 计算协方差矩阵 $XX^T$ 并特征值分解
  3. 取最大 $d$ 个特征向量为投影矩阵
- PCA: 最佳描述特征
- LDA: 最佳分类特征

## 非线性降维

### 核化线性降维

- KPCA
- KLDA

### 流行学习

Isomap

- 只考虑局部距离
- 算法
  1. 最短路径算法求出任意两点距离
  2. 带入 MDS

LLE (Locally Linear Embedding 局部线性嵌入)

- 只考虑领域内样本间的线性关系，在低维空间重构权值

- 算法

  1. 确定每个点的 $k$ 近邻 $Q_i$

  2. 根据下式求出 $\omega_{ij},j\in Q_i$,且 $\omega_{ij}=0$ if $j\notin Q_i$
     
     
     $$
     \begin{equation}
     \begin{aligned}
     \min_{\omega_1,\omega_2,\cdots,\omega_m}\sum_{i=1}^m\Vert x_i& \sum_{i\in Q_i}\omega_{ij}x_j\Vert_2^2 \\
     s.t.\sum_{j\in Q_i}\omega_{ij}& =1 \\
     \end{aligned}
     \end{equation}
     $$
     
  3. 对 $M=(I-W)^T(I-W)$ 特征值分解，最小的 $d'$ 个特征值为投影 $Z$









