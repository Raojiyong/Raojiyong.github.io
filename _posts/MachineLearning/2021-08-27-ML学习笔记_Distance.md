---
title: ML Distance
author: raojiyong
date: 2021-08-27 19:00:00 +0800
categories: ["2021","08"]
tags: [Machine Learning,notes]
math: true
mermaid: true
---

### 距离

- 正定性
- 对称性
- 三角不等式

#### 有序距离

- 闵科夫斯基距离: $l=(\sum_{i=1}^n\vert x_i-y_i\vert^p)^\frac1p$
  - 切比雪夫距离: $l_{\infty}=\max_{i=1}^n\vert x_i-y_i\vert$
  - 欧几里得距离: $l_2=\sqrt{\sum_{i=1}^n\vert x_i-y_i\vert^2}$
  - 曼哈顿距离: $l_1=\sum_{i=1}^n\vert x_i-y_i\vert$
  - 加权闵科夫斯基距离: $l=(\sum_{i=1}^n\omega_i\vert x_i-y_i\vert^p)^\frac1p$
- 马氏距离: $d(\vec{x},\vec{y})=\sqrt{(\vec{x}-\vec{y})^TS^{-1}(\vec{x}-\vec{y})}$
  - $S$ 协方差矩阵
  - $\mathrm{dist}_{mah}^2(x_i,x_j)=(x_i-x_j)^TM(x_i-x_j)=\Vert x_i-x_j\Vert_M^2$, 度量矩阵 $M$ 为半正定矩阵。
  - $M=PP^T$
    -  $\Vert x_i-x_j\Vert_M=\Vert P^Tx_i-P^Tx_j\Vert$
- 余弦距离: $d(x,y)=\frac{<x,y>}{\vert x\vert\vert y\vert}$

#### 离散距离

##### 簇

- VDM (Value Difference Metric)
  - $m_{u,a}$: 在属性 $u$ 上取值为 $a$ 的样本数
  - $m_{u,a,i}$: 第 $i$ 个样本簇在属性为 $a$ 的样本数
  - $\text{VDM}_p(a,b)=\sum_{i=1}^k\vert \frac{m_{u,a,i}}{m_{u,a}}-\frac{m_{u,b,i}}{m_u,b}\vert$
  - $\text{MinkovDM}_p(a,b)={(\sum\vert x_{iu}-x_{ju}\vert^p+\sum\text{VDM}_p(x_{iu},x_{ju}))^{\frac1p}}$

##### 字符串

- 海明距离
- Lee 距离
- Levenshtein (编辑距离)

$$
\text{lev}(a,b)=\begin{cases}
\max(i,j)\qquad \text{if}\ \min(i,j)=0\newline 
\min\begin{cases}\text{lev}_{a,b}(i-1,j)+1 \newline
\text{lev}_{a,b}(i,j-1)+1 \newline
\text{lev}_{a,b}(i-1,j-1)+1_{a_i\neq b_j} \newline
\end{cases} \qquad \text{otherwise}
\end{cases}
$$

#### 非度量距离

不满足三角不等式 (相似度度量无需满足三角不等式)

#### 两组点集的相似程度

- Hausdorff 距离
  - $\text{dist}_H(X,Z)=\max(\text{dist}_h(X,Z),\text{dist}_h(Z,X))$
  - $\text{dist}_h(X,Z)=\max_{x\in X}\min_{z\in Z}\Vert x-z\Vert_2$

#### NCA

Neighbourhood Component Analysis 近邻成分分析

- 近邻分类器中 $x_j$ 对 $x_i$ 分类结果影响概率为: $p_{ij}=\frac{e^{-\Vert x_i-x_j\Vert_M^2}}{\sum_le^{-\Vert x_i-x_j\Vert_m^2}}$
- $x_i$ LOO 正确率: $p_i=\sum_{j\in \Omega_i}p_{ij},\Omega_i$ 为相同类别下标
- 训练集 LOO 正确率: $\sum_{i=1}^mp_i=\sum_{i=1}^m\sum_{j\in \Omega_i}p_{ij}$
- $\min_p1-\sum_{i=1}^m\sum_{j\in \Omega_i}\frac{\exp(-\Vert P^Tx_i-P^Tx_j\Vert_2^2)}{\sum_l\exp(-\Vert P^Tx_i-P^Tx_l\Vert_2^2)}$

### 领域知识

必连约束 $\mathcal{M}$,勿连约束 $\mathcal{C}$

$$\begin{equation}
\begin{aligned}
\min_{M}&\sum_{(x_i,x_j)\in\mathcal{M}}\Vert x_i-x_j\Vert_M^2 \notag \\
s.t. &\sum_{(x_i,x_k)\in\mathcal{C}}\Vert x_i-x_k\Vert_m \geq1 \notag\\
&M\succeq 0
\end{aligned}
\end{equation}$$

#### LMNN

Large Margin Nearest Neighbors

- $k$ 个目标邻居相近，入侵样本远离

  - 目标邻居：最近的同类别样本

  - 入侵样本：最近中的非同类样本

$$
\begin{align}
\min\ast M&\sum_{i,j\in N\ast i}d(x_i,x_j)+\sum_{i,j,l}\xi_{ijl} \notag \\
s.t.&\forall_{i,j\in N_k,l,yl\neq y_i}d(x_i,d_j)+1\leq d(x_i,x_l)+\xi_{ijl} \notag \\
&\xi_{ijl}\geq0 \notag \\
&M \succeq0 \notag \\
\end{align}
$$



