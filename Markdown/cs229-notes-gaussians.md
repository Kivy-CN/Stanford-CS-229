# CS229 课程讲义中文翻译
CS229 Section notes

|原作者|翻译|
|---|---|
|Chuong B. Do|[XiaoDong_Wang](https://github.com/Dongzhixiao) |


|相关链接|
|---|
|[Github 地址](https://github。com/Kivy-CN/Stanford-CS-229-CN)|
|[知乎专栏](https://zhuanlan。zhihu。com/MachineLearn)|
|[斯坦福大学 CS229 课程网站](http://cs229。stanford。edu/)|
|[网易公开课中文字幕视频](http://open。163。com/movie/2008/1/M/C/M6SGF6VB4_M6SGHFBMC。html)|


### 多元高斯分布

#### 介绍

我们称一个概率密度函数是一个均值为$\mu\in R^n$，协方差矩阵为$\Sigma\in S_{++}^n$$^1$的一个**多元正态分布（或高斯分布）(multivariate normal (or Gaussian) distribution)，** 其随机变量是向量值$X=[X_1\dots X_n]^T$，该概率密度函数$^2$可以通过下式表达：

<blockquote><details><summary>上一小段上标1,2的说明（详情请点击本行）</summary>

1 复习一下线性代数章节中介绍的$S_{++}^n$是一个对称正定的$n\times n$矩阵空间，定义为：

$$
S_{++}^n=\{A\in R^{n\times n}:A=A^T\quad and\quad x^TAx>0\quad for\quad all\quad x\in R^n\quad such\quad that\quad x\neq 0\}
$$

2 在我们的这部分笔记中，不使用$f_X(\bullet)$（如概率论注释一节所述），而是使用符号$p(\bullet)$代表概率密度函数。

</details></blockquote>

$$
p(x;\mu,\Sigma)=\frac{1}{(2\pi)^{n/2}|\Sigma|^{1/2}} exp(-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu))
$$

我们可以将其简写做$X\sim\mathcal{N}(\mu,\Sigma)$。在我们的这部分笔记中，我们描述了多元高斯函数及其一些基本性质。

#### 1. 与单变量高斯函数的关系

回忆一下，**一元正态分布（或高斯分布）(univariate normal (or Gaussian) distribution)** 的密度函数是由下式给出：

$$
p(x;\mu,\sigma^2)=\frac 1{\sqrt{2\pi}\sigma}exp(-\frac 1{2\sigma^2}(x-\mu)^2)
$$

这里，指数函数的自变量$-\frac 1{2\sigma^2}(x-\mu)^2$是关于变量$x$的二次函数。此外，抛物线是向下的，因为二次项的系数是负的。前面的系数$\frac 1{\sqrt{2\pi}\sigma}$是不依赖$x$的常数。因此，我们可以简单地把这个系数当作保证下面的式子成立的“标准化因子”(normalization factor)。

$$
\frac 1{\sqrt{2\pi}\sigma}\int_{-\infin}^{\infin} exp(-\frac 1{2\sigma^2}(x-\mu)^2)=1
$$

![](https://github.com/Kivy-CN/Stanford-CS-229-CN/blob/master/img/cs229notegf1.png?raw=true)

在多元高斯概率密度函数的情况下，指数函数的自变量$-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu)$是一个以向量形式的$x$为变量的**二次形(quadratic form)**。因为$\Sigma$是正定矩阵，并且任何正定矩阵的逆也是正定的，那么对于任何非零向量$z$，有$z\Sigma^Tz>0$。这就暗示了任何向量$x\neq\mu$，有：

$$
(x-\mu)^T\Sigma^{-1}(x-\mu)>0 \\
-\frac 12(x-\mu)^T\Sigma^{-1}(x-\mu)<0
$$

就像在单变量的情况下，你可以把指数函数的参数看成是一个开口向下的二次曲线。指数函数前面的系数（即，$\frac{1}{(2\pi)^{n/2}|\Sigma|^{1/2}}$）是一个比单变量情况下更复杂的一种形式。但是，它仍然不依赖于$x$，因此它只是一个用来保证下面的式子成立的标准化因子：

$$
\frac{1}{(2\pi)^{n/2}|\Sigma|^{1/2}}\int_{-\infin}^{\infin}\int_{-\infin}^{\infin}\dots\int_{-\infin}^{\infin}exp(-\frac{1}{2}(x-\mu)^T\Sigma^{-1}(x-\mu))dx_1dx_2\dots dx_n=1
$$