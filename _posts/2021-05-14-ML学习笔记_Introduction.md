---
usemathjax: true
title: ML Introduction
author: raojiyong
date: 2021-05-14 15:00:00 +0800
categories: ["2021", "05"]
tags: notes
---

## 机器学习

- 机器学习要素
  - 模型
  - 学习准则
  - 优化算法
  
- 数据集：$D=x_1,x_2,...,x_m$
  - 通常假设全体样本服从一个未知分布$\mathcal{D}$,且采样$i.i.d$
  
- 归纳偏好
  - No Free Lunch Theorem
  - Occam's Razor
  - Ugly Ducking Theorem
  
- all vectors are assumed to be column vectors

- $N$ number of input, $p$ number of features

- 训练集$X_{N_\times p}$

  - $i$-th row $x_i^T$:length $p$
  - $j$-th column $x_j$ :length N
  - input vector: $X_{p\times 1}$
  - $X^T=(X_1,X_2,\cdots,X_p),X_i $ is a scalar

- $y_{N_\times 1}$

  - $Y \in R$
  - $Y_{N_\times 1}$, each row has one 1

- $(X_1,X_2)$: 行并列

- $(X_1^T,X_2^T)$: 列并列

- 偏差-方差分解：

  $E(f;D)=bias^2(x)+var(x)+c^2=(\overline f(x)-y)^2+E_D((f(x;D)-\overline f(x))^2)+E_D((y_D-y)^2)$

## 评估方法

- 留出法
- cross validation
  - 将数据集分层采样划分为 $k$ 个大小相似的互斥子集，每次用 $k-1$ 个子集的并集作为训练集，余下的子集作为行为测试集，最终返回 $k$ 个测试结果的均值。
  - $k$ 最常用的取值是 10
  - LOO(leave-one-out): k=1.
- bootstrapping: 样本不被选到的概率=$\lim_{m \to \infty}(1-\frac {1}{m})^m=\frac{1}{e}=0.368.$

## 模型评估指标

- T,F: 分类正确与否
- R,N: 预测结果

**Regression**

- 均方误差:$E(f;D)=\frac{1}{m}\sum_{i-1}^m(f(x_i)-y_i)^2$

**Classification**

| 指标         |                                                              |
| ------------ | ------------------------------------------------------------ |
| accuracy     | $\frac{TP+TN}{m}$                                            |
| precision    | $\frac{TP}{TP+FP}$                                           |
| recall       | $\frac{TP}{TP+FN}$                                           |
| macro-P      | $\frac{1}{n}\sum _{i=1}^n P_i$                               |
| macro-R      | $\frac{1}{n}\sum _{i=1}^n R_i$                               |
| micro-P      | $\frac{TP}{TP+FP}$                                           |
| micro-R      | $\frac{TP}{TP+FN}$                                           |
| 平衡点(BEP)  | P-R曲线上 P=R 的点                                           |
| F1           | $\frac{2PR}{P+R}$调和平均更重视较小值                        |
| $F_\beta$    | $\frac{1}{F_\beta}=\frac{1}{1+\beta ^2}(\frac{1}{P}+\frac{\beta^2}{R}),\beta>1,R $ counts more |
| TPR          | R                                                            |
| FPR          | $\frac{FP}{TN+FP}$                                           |
| ROC          | TPR-FPR 图 (Receiver Operating Characteristic)               |
| AUC          | (Area Under Curve) $\frac{1}{2}\sum_{i=1}^{m-1}(x_{i+1}-x_i)(y_{i+1}+y_i)$ |
| FPR          | 1-TPR                                                        |
| cost curve   | 横轴为正例概率代价，纵轴为归一化代价                         |
| Ranking Loss | $l$=1-AUC                                                    |

**Ranking**

- One query  $r\to$ One permutation $\pi$
- One query  $r\to$  retrieved documents $R(r)$
- 

## 多分类

- OvO：储存开销于测试时间偏大
- OvR：训练时间偏大
- MvM：
  - Error Correcting Output Codes(ECOC)
    - 编码：二元码，三元码
    - 解码：将距离最小的编码所对应的类别作为预测结果
- argmax: $y=arg max_{c=1}^C f_c(x;w_c)$

## 类别不平等

- 欠采样
- 过采样
- 阈值移动：$\frac{y}{1-y} > \frac{m^+}{m^-}$

## 假设检验

- 二项检验
  - 二项分布：$P(\hat \epsilon;\epsilon)=\binom{m}{\hat\epsilon m}\epsilon^{\hat\epsilon m}(1-\epsilon)^{m-\hat\epsilon m}$
  - 假设：$\epsilon \le \epsilon_0$
  - 临界值$\bar\epsilon=max\  \epsilon$  s.t. $\sum_{i=\epsilon_0 \times m+1}^m \binom{m}{i}\epsilon^i(1-\epsilon)^{m-i}$
- t 检验
  - 检验值：$\tau_t=\frac{\sqrt{k}(\mu-\epsilon_0)}{\sigma}$
- 交叉验证 t 检验
  - 差值：$\Delta_i=\epsilon_i^A-\epsilon_i^B$
  - $\tau_t=\vert \frac{\sqrt{k}(\mu-\epsilon_0)}{\sigma}\vert$
  - 假设检验前提：测试错误率为泛化错误率独立采样
    - 5$\times$2交叉验证（为缓解不同训练轮次训练集的重叠问题，5次2折交叉验证）
- McNemar 检验
  - $e_{ij}:i$ 指示算法 $A$ 预测正确与否，$j$ 指示算法 $B$ 预测正确与否
  - 假设：$e_{01}=e_{10}$
  - $\vert e_{01}-e_{10}\vert \sim N(1,e_{01}+e_{10})$
  - 统计检验量：$\tau=\frac{(\vert e_{01}-e_{10}\vert -1)^2}{ e_{01}-e_{10}}\sim \chi^2(1)$
- Friedman 检验：多个数据集对多个算法比较
  - 根据测试性能赋予序值，求得平均序值
  - 假设：算法性能全部相同
  - $\tau_\chi^2=\frac{12N}{k(k+1)}(\sum_{i=1}^kr_i^2-\frac{k(k+1)^2}{4})$,当 k, N 较大时，服从$\chi^2(k-1)$ 分布
  - $\tau_F=\frac{(N-1)\tau_\chi^2}{n(K-1)-\tau_\chi^2}\sim F(k-1,(k-1)(N-1))$
- Nemenyi 检验：算法性能全部相同假设被拒绝后进一步区分各算法
  - CD=$q_\alpha \sqrt{\frac{k(k+1)}{6N}},q_\alpha$ 为 Tukey 分布临界值
  - 若两个算法平均序值之差超出临界值域 CD，则以相应置信度拒绝两个算法性能相同

