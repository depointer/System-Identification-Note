# 遗传算法及其在辨识中的应用

## 1. 引言
J H.Holland 1975

- 进化计算
  - GA - Generic Algorithm
  - PSO - particle swarm optimization
  - Ants
  - Bee
  - 萤火虫
  - 狼群（捕食）
  - 细菌（吸收养分）
  - 免疫算法

- 问题
  - 收敛性
  - 不能在线


- 特点
  - 群体化
  
- 个体-染色体chromosome
- 组成：个体——基因
- 评价：优劣
- 机制：优胜劣汰
- 繁殖：优$\rightarrow$更优

## 2. GA基本框架

### 2.1. 一般优化vs遗传算法
一般优化
$$
x(0)\xrightarrow{\Delta x} x(1)\xrightarrow{\Delta x} x(2)\xrightarrow{\Delta x}\cdots\xrightarrow{\Delta x}x(M)
$$
$$
J(0)<J(1)<J(2)\cdots
$$

遗传算法

$$
P(t)=\{x_1(t)\ x_2(t)\ \cdots\ x_N(t) \}
$$

$$
P(0)\rightarrow P(1)\rightarrow P(2)\rightarrow\cdots\rightarrow P(L)
$$
缺点：不能保证收敛
### 2.2 评价函数

### 2.3 操作
- 概率机制
  - 选择

### 2.4 基本要素
1. 遗传表示
2. 评价函数 - 适应度函数
3. 建立种群
4. 操作(遗传算法的改进主要在这里)
5. 参数(启发式算法，对参数十分敏感)

### 2.5 基本流程

- 遗传算法
    1. 种群初始化
    2. 评价每个个体
    3. 选择
    4. 繁殖

```flow
st=>start: 遗传算法
e=>end: 最好染色体即为所求解

op1=>operation: 种群初始化
op2=>operation: 评价每个染色体
op3=>operation: 选择
op4=>operation: 繁殖
cond1=>condition: 是否满足终止条件


st->op1->op2->op3->op4->cond1
cond1(no,right)->op2
cond1(yes)->e
```

### 2.6 GA在辨识中的应用
考虑$y=f(u,\theta)$，$f$已知，采样$\{u(k) y(k) \} $

$$
J = TODO
$$

###### 1. 遗传表示
0-1 二进制
假设$\theta=[a_1\ a_2\ \cdots\ a_n]^T$
$$a_i\in[L_i\ V_i]$$
按$10^{-b}$离散化

$$
2^{m_i-1}<U_i\times 10^b-L_i\times10^b<2^{m_i}
$$

###### 2. 适应度函数
$$
g(\theta)=\frac{1}{1+J(\theta)}
$$
###### 3. 种群初始化
- 随机初始化$N$个m位0-1，记为$\theta_i(0), i=1,2,\cdots,N$.

###### 4. 选择
$$
p_i\propto g(\theta_i)
$$
$$
p_i= \frac{g(\theta_i)}{\sum^N_{j=1}{g(\theta_j)}}
$$
>- 遗传算法比神经网络初值敏感性弱
>- 早熟，某些个体适应度函数过大，但是为局部最优

###### 5. 交叉(corssover)

针对个体i
指定$p_c\in[0.5,0.9]$
对每个个体按均匀分布生成随机数$r_i\in[0,1]$。

如果$r_i<p_c$选择两两配对

配对的个体前m位不变，余下的交换


###### 6. 变异(mutation)
针对基因，指定变异概率$p_m\in[0.0001,0.001]$
对个体每一位按均匀分布生成随机数$r_i\in[0,1]$。

如果$r_i>p_m$该位不变，否则翻转

- 保护策略：当前适合度函数足够好的个体直接进入下一代
- 自适应变异：评价交叉对的相似度，如果相似度高，下一代就提高变异概率，否则减小。
###### 7. 终止条件
当前种群中最好的个体适应度函数足够好了



## 3. 特点
-  优点
   - 适用范围广
   -  适合约束强的问题，硬约束
   -  鲁棒性强
   -  相比于迭代算法，全局优化能力强
   -  初始值不敏感
- 缺点
  - 可能陷入局部最优
  - 对参数敏感
  - 概率算法，解的可重现性弱
