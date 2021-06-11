---
title: 群论学习笔记(.......ing)
tags: Group-Theory
layout: article
license: true
toc: true
key: a20210415
header:
  theme: dark
  background: 'linear-gradient(135deg, rgb(34, 139, 87), rgb(139, 34, 139))'
article_header:
  type: overlay
  theme: dark
  background_color: '#123'
  background_image: false
pageview: true
sitemap: true
mathjax: true
author: YuXuan
show_author_profile: true
---
学习群论有一段时间了, 这里想结合一些工具, 并通过一些书籍阅读来将自己所学到的内容整理一下, 同时加深一下自己对这些知识内容的理解.
{:.info}
<!--more-->

# 共轭
一个元素$a,b,c$是群$\mathcal{G}$的群元$(a,b,c)\in\mathcal{G}$,加入下列关系成立

$$a=c\circ b\circ c^{-1}\label{eq1}$$

那么就说群元$a$与$b$之间是共轭的.**上式中的$\quad\circ\quad$代表的是群元的操作**.
# 类
利用(\ref{eq1})的关系,将所有与群元$b$共轭的群元划分成一组,那么这一组叫做一个类.

$$\mathcal{C}_{a}=\left\{a_{i} \mid a, b \in \mathcal{G} \wedge a_{i}=b \circ a \circ b^{-1} \wedge a \text { fixed }\right\}$$

# 陪集
假设$\mathcal{U}$是群$\mathcal{G}$的子群,$a$是$\mathcal{G}$中的元素,那么$a\mathcal{U}$代表元素$a$和群$\mathcal{U}$中的每一个元素相操作,形成一个集合,叫做左陪集.那么相应的$\mathcal{U}a$就叫做右陪集

$$\begin{array}{ll}
a \mathcal{U}=\{a \circ p \mid p \in \mathcal{U} \subseteq \mathcal{G}\}, & a \in \mathcal{G} \\
\mathcal{U} a=\{p \circ a \mid p \in \mathcal{U} \subseteq \mathcal{G}\}, & a \in \mathcal{G}
\end{array}$$

**陪集有一个很重的性质：任意两个陪集，它们要么是完全相同的，要么完全没有公共元素；也就是说群中的一个群元，它只可能属于一个陪集。这个性质对左右陪集都是成立的。**

![png](/assets/images/GroupTheory/coset1.png)

# 不变子群
首先给出书上不变子群的定义

![png](/assets/images/GroupTheory/invsub.png)

解释一下,就是首先这个子群$\mathcal{S}$的所有元素,在$x\in\mathcal{G}$的共轭操作下,还是它自己,这里要强调的是,这个关系要对所有的$x\in\mathcal{G}$都成立才可以,这就是不变子群的特殊之处.

# 商群(Factor Group)
![png](/assets/images/GroupTheory/factor.png)

既然前面提到了,对于陪集来说,它们之间要么是相同的,要么是完全没有交集,利用这个性质,可以简单的将陪集想象成基矢,类似于坐标空间中的基矢,只不过这个时候的基矢就是我们提到的陪集,那么就可以将整个群在这些基矢上进行分解,也就是图中(3.17)所表示的含义,至于这个基矢的数量可以参考陪集中定理8的第六条.

将这些分解的陪集整合到一起,可以形成一个集合$\mathcal{G}/\mathcal{S}=\{g_1\mathcal{S},g_2\mathcal{S},\dots,g_N\mathcal{S}\}$,给这个集合起个名字叫做**商集**.

在上面对群$\mathcal{G}$进行基矢分解的时候,选取的是它的任意子群$\mathcal{S}$,前面已经介绍过不变子群的概念,那么现在就将这个分解在不变子群上进行,不变子群利用特殊标记$\mathcal{N}$来表示.

当这个分解在不变子群$\mathcal{N}$上进行时,会发现最后产生的这个**商集**它又会存在一些额外的性质,简单的说就是这个集合中的元素满足构成**群**的四个基本条件,所以就称之为**商群**.最开始学群论的时候,所接触的群元都是一个一个的操作元,但是商群在这里就有一些不同,从上面构成**商集**的过程来看,商群中的每一个群元(操作),其实对应的是群$\mathcal{G}$的一些群元(操作)的集合,也就是说群$\mathcal{G}$中的多个操作,现在从商群的角度看其实就是商群中的一个群元(操作),好像形成了多对一的映射关系(这里仅仅就是我从群元关系的角度进行的理解,我也不确定用映射这个词是否是正确的).
{:.success}

接下来就利用[GTPack](http://gtpack.org/)这个包,来计算一个商群的实例.关于这个包的下载和安装,可以看我这篇[Mathematica群论工具GTPack安装及使用](https://yxli8023.github.io/2020/08/06/Group.html)博客

![png](/assets/images/GroupTheory/factor2.png)

![png](/assets/images/GroupTheory/factor3.png)

计算的代码可以[点击这里下载](/assets/data/1005.nb)

# Homomorphism
存在两个群$G$与$G^{'}$,如果在$G$与$G^{'}$有一个映射关系$\theta$且仍然满足群元素的运算关系,那么这个映射称为同态(Homomorphism).

$$(\theta A_i)(\theta A_j)=\theta(A_iA_j)\quad \text{for all }A_i,A_j\in G$$

阶数较小的群称为阶数较大的群的同态像(homomorph). 把$G$中映射到$G^{'}$单位元素上的所有元素的集合, 称为同态核(kernel of the homomorphism).

# Isomorphism
如果这个映射使得群$G$与$G^{'}$中的元素满足一一对应关系, 那么此时的$\theta$叫做同构(Isomorphism), 两个群之间是同构的(isomorphic).

# automorphism
如果两个群$G$与$G^{'}$是完全相同的, 那么也就是$\theta$是一个群到自身的映射, 那么这种映射称为自同构(automorphism).

如果$\theta$是自同构映射, 且映射满足

$$\theta G=XGX^{-1};\text{for }X\in G$$

此时可以看出自同构是等价于共轭的, 那么这种情况称为内自同构(inner automorphism), 其余的情况就称为外自同构(outer automorphisms).

## 实例
If $G$ = $G_6$ and $G^{'}= G_2 = \{E,A^{'}\}$, then the mapping

$$\theta(E)= \theta(D)= \theta(F)= E\\ \theta(A)= \theta(B)= \theta(C)= A^{'}$$

is a homomorphism of $G_6$ onto $G_2$.

The groups $C_{3v}$, $D_3$ and $S_3$ are isomorphic: They have the same order and share the same multiplication table.

If $\theta(E)= E, \theta(A)= B, (B)= C, \theta(C)= A, \theta(D)= F$, and $\theta(F)= D$, the mapping is an automorphism of $G_6$ onto itself.