---
title: ML DecisionTree
author: raojiyong
date: 2021-05-23 15:00:00 +0800
categories: ["2021","05"]
tags: notes, machine learning
math: true
mermaid: true1
---

### 决策树基本算法

- 当前节点包含样本全部同类：标记为某类
- 当前样本属性值为空/取值相同：标记为最多一类
- 属性划分选择
- 为属性每个值分配一个结点继续执行算法
  - 若其属性值上为空则标记为当前最多一类

递归过程，分治

### 划分选择

| 指标名称            | 指标                                                         | 辅助函数                                                     | 例子 | remark                                                       |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| 信息增益(Info gain) | $\mathrm{Gain}(D,a)=\mathrm{Ent}(D)-\sum_{v=1}^V\frac{\vert D^v\vert}{\vert D\vert}\mathrm{Ent}(D^v)$ | 信息熵$\mathrm{Ent}(D)=-\sum_{k=1}^{\vert y\vert}p_klog_2p_k$ | ID3  | 对可取值数目较多的属性有偏好                                 |
| Gain ratio          | $\mathrm{Gain\_ratio}(D,a)=\frac{\mathrm{Gain}(D,a)}{\mathrm{IV}(a)}$ | 固有值$\mathrm{IV}(a)=-\sum_{v=1}^V\frac{\vert D^v\vert}{\vert D\vert}log_2\frac{\vert D^v\vert}{\vert D\vert}$ | C4.5 | 从候选划分中找出信息增益高于平均水平的属性，再从中选择增益率最高的 |
| Gini ratio          | $\mathrm{Gini_index}(D,a)=\sum_{v=1}^V\frac{\vert D^v\vert}{\vert D\vert}\mathrm{Gini}(D^v)$ | $\mathrm{Gini}(D)=1-\sum_{k=1}^{\vert Y\vert}p_k^2$          | CART | Gini指数为随机抽取两个样本类别标记不一致的概率，越小纯度越高 |

### 剪枝处理

| 方法   | 指标      | 过拟合         | 欠拟合       | 训练时间 |
| :----- | --------- | -------------- | ------------ | -------- |
| 预剪枝 | precision | 降低过拟合风险 | 有欠拟合风险 | 较小     |
| 后剪枝 | precision | 降低过拟合风险 | 欠拟合风险小 | 较长     |

### 连续与缺失值

- 连续属性离散化(二分法)
  - $T_a=\frac{a^i+a^{i+1}}2 \vert\ 1\le i\le n-1$

- 缺失值
  - $\tilde{D}:D$在属性 $a$ 上没有缺失值的样本子集
  - $\tilde{D}^v:D$中属性 $a$ 上取值为 $a^v$ 的样本子集
  - $\tilde{D}_k:\tilde{D}$ 类别中为 $k$ 的样本子集
  - $\omega_x:$ 每个样本的权重
  - $\rho=\frac{\sum_{x\in\tilde{D}}\omega_x}{\sum_{x\in D}\omega_x}$ 对属性 $a$ ，$\rho$ 表示无缺失样本所占比例
  - $\tilde{p_k}=\frac{\sum_{x\in\tilde{D}_k}\omega_x}{\sum_{x\in D}\omega_x}$ 对属性 $a$，$\tilde{p_k}$ 表示无缺失值样本中第 $k$ 类的占比
  - $\tilde{r_v}=\frac{\sum_{x\in\tilde{D}^v}\omega_x}{\sum_{x\in D}\omega_x}$ $\tilde{r_v}$表示无缺失值样本中在属性 $a$ 上取值 $a^v$ 的占比
  - $\mathrm{Ent}(\tilde{D})=-\sum_{k=1}^{\vert Y\vert}\tilde{p_k}log_2\tilde{p_k}$
  - $\mathrm{Gain}(D,a)=\rho*\mathrm{Gain}(\tilde{D},a)=\rho*\Bigl(\mathrm{Ent}(\tilde{D})-\sum_{v=1}^V\tilde{r_v}\mathrm{Ent}(\tilde{D^v})\Bigr)$

### 多变量决策树

- 每个非叶节点用 $\sum_{i=1}^d\omega_ia_i=t$ 的线性分类器，是对属性的线性组合进行测试。
- 特征预处理