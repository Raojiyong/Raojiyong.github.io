---
title: ML Clustering
author: raojiyong
date: 2021-08-04 15:00:00 +0800
categories: ["2021","08"]
tags: [notes,Machine Learning]
math: true
mermaid: true
---

### 性能度量

- 性能度量，有效性指标 validity index
- 外部指标：与某个参考模型比较
  - 簇划分：$\mathcal{C}=C_1,C_2,\cdots,C_k$，参考模型簇划分 $\mathcal{C^*}=\{C_1^*,C_2^*,\cdots,C_s^*\},\lambda,\lambda^*$ 分别为两者的簇标记向量，定义
    - $a=\vert\text{SS}\vert,\text{SS}=\{(x_i,x_j)\ \vert\ \lambda_i=\lambda_j,\lambda_i^*=\lambda^*_j,i\lt j\}$
    - $b=\vert\text{SD}\vert,\text{SD}=\{(x_i,x_j)\ \vert\ \lambda_i=\lambda_j,\lambda_i^*\neq\lambda^*_j,i\lt j\}$                                                                                  
    - $c=\vert\text{DS}\vert,\text{DS}=\{(x_i,x_j)\ \vert\ \lambda_i\neq\lambda_j,\lambda_i^*=\lambda^*_j,i\lt j\}$
    - $d=\vert\text{DD}\vert,\text{DD}=\{(x_i,x_j)\ \vert\ \lambda_i\neq\lambda_j,\lambda_i^*\neq\lambda^*_j,i\lt j\}$
    - $a+b+c+d=\frac{m(m-1)}2$
  - JC (Jaccard Coefficent)
    - $\text{JC}=\frac a{a+b+c}$
  - FMI (Fowlkes and Mallows Index)
    - $\text{FMI}=\sqrt{\frac a{a+b}\cdot\frac a{a+c}}$
  - RI (Rand Index)
    - $\text{RI}=\frac{2(a+d)}{m(m-1)}$
- 内部指标
  - 簇划分: $\mathcal{C}=C_1,C_2,\cdots,C_k$
    - $\text{avg}(C)=\frac 2{\vert C\vert(\vert C\vert-1)}\sum_{1\leq i\lt j\leq\vert C\vert}\text{dist}(x_i,x_j)$ 簇内样本平均距离
    - $\text{diam}(C)=\max_{1\leq i\lt j\leq\vert C\vert}\text{dist}(x_i,x_j)$ 簇内样本间最远距离
    - $d_{min}(C_i,C_j)=\min_{x_i\in C_i,x_j\in C_j}\text{dist}(x_i,x_j)$ 
    - $d_{cen}=\text{dist}(\mu_i,\mu_j)$ 簇$C_i$与簇$C_j$中心点的距离
  - DBI (Davies Bouldin Index)
    - $\text{DBI}=\frac1k\sum_{i=1}^k\max_{j\neq i}(\frac{\text{avg}(C_i)+\text{avg}(C_j)}{d_{cen}(C_i,C_j)})$ 越小越好
  - DI (Dunn Index)
    - $\text{DI}=\min_{1\leq i\leq k}(\min_{j\neq i}(\frac{d_{\text{min}(C_i,C_j)}}{\max_{1\leq l\leq k}\text{diam}(C_l)}))$ 越大越好

### 原型聚类

- SOM: self-organizing maps

#### k-means

Learning Vector Quantization 学习向量量化

- 利用样本监督信息
- 每次迭代，每个样本对其最近的原型向量根据标记一致性做推动/吸引
- 每个原型向量 $p_i$ 定义了与之相关的一个区域 $R_i$，形成了对样本空间的 Voronoi tessellation

#### 高斯混合聚类

- 高斯混合分布：$p_M(x)=\sum_{i=1}^h\alpha_i\cdotp(x\vert \mu_i.\sum_i),\ \sum_{i=1}^k\alpha_i=1$
- EM 算法求解
  - $\text{LL(D)}=\ln(\prod\limits_{j=1}^mp_M(x_j))=\sum_{j=1}^m\ln(\sum_{i=1}^k\alpha_ip(x_j\vert \mu_i,\sum_i))$
  - $\text{E:}\gamma_{ji}=p_M(z_j=i\vert x_j)$
  - $\text{M}$
    - $\mu_i'=\frac{\sum_{j=1}^m\gamma_{ji}x_j}{\sum_{j=1}^m\gamma_{ji}}$ 新均值向量
    - $\sum_i'=\frac{\sum_{j=1}^m\gamma_{ji}(x_j-\mu_i')(x_j-\mu_i')^T}{\sum_{j=1}^m\gamma_{ji}}$ 新协方差矩阵
    - $\alpha_i'=\frac{\sum_{j=1}^m\gamma_{ji}}{m}$ 新混合系数

### 密度聚类

假设聚类结构能通过样本分布的紧密程度确定

#### DBSCAN 

- $\epsilon$-邻域：$N_\epsilon(x_j)={x_i\in D\vert \text{dist}(x_i,x_j)\leq\epsilon}$ 样本集中与$x_j$的距离不大于$\epsilon$ 的样本
- 核心对象：$x_j,\ \vert N_\epsilon(x_j)\vert\ge\text{MinPts}$
- directly density-reachable: $x_j\in N_\epsilon(x_i)$且$x_i$ 为核心对象，则$x_j$由$x_i$密度可达（无对称性）
- density-reachable
- density-connected: $\exists x_k,x_i,x_j$均由$x_k$密度可达
- 簇 为满足下列性质的最大集合
  - connectivity: $x_i\in C,x_j\in C$ 则 $x_i,x_j$ 密度相连
  - maximality: $x_i\in C,x_j$ 由 $x_i$ 密度可达，则 $x_j\in C$
- 算法：
  1. 找出所有核心对象
  2. 对每个核心对象求 $X=x'\in D\vert x'$ 由 $x$ 密度可达

#### DIANA

top-down

### 层次聚类

自底向上或者自顶向下

#### AGNES

agglomerative nesting

- 自底向上
- 起初每个样本点为一个簇
- 不断合并最近两个簇

| name                    | d    |
| ----------------------- | ---- |
| single-linkage 单链接   | min  |
| complete-linkage 全链接 | max  |
| average-linkage 均链接  | avg  |