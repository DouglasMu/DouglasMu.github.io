---
layout: post
title:  算法面试
categories: algorithm
tags:  算法
author: Keyon
---
* content
{:toc}


<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default">
</script>

#### 为什么要做数据的归一化
* 提升模型的收敛速度

    如下图，x1的取值为0-2000，而x2的取值为1-5，假如只有这两个特征，对其进行优化时，
    会得到一个窄长的椭圆形，导致在梯度下降时，梯度的方向为垂直等高线的方向而走之字形路线，
    这样会使迭代很慢，相比之下，右图的迭代就会很快数据归一化后，最优解的寻优过程明显会变得平缓，
    更容易正确的收敛到最优解。
    ![收敛速度](https://images2015.cnblogs.com/blog/743682/201511/743682-20151108152327539-2039269197.png)


* 提升模型的精度 

    归一化的另一好处是提高精度，这在涉及到一些距离计算的算法时效果显著，
    比如算法要计算欧氏距离，上图中x2的取值范围比较小，
    涉及到距离计算时其对结果的影响远比x1带来的小，所以这就会造成精度的损失。
    所以归一化很有必要，他可以让各个特征对结果做出的贡献相同。






* 常用的归一化方法及归一化方法的选择

    常用的归一化方法有两个：
    
    ①线性归一化
    
    $$ X_norm = \frac{X-X_min}{X_max-X_min} $$
    
    ②0均值标准化
    
     $$ z = \frac{x-μ}{σ} $$
     
     其中，μ、σ分别为原始数据集的均值和方法。该种归一化方式要求原始数据的分布可以近似为高斯分布，
     否则归一化的效果会变得很糟糕。
    

* 关于归一化方法的选择

    1） 在分类、聚类算法中，需要使用距离来度量相似性的时候、或者使用PCA技术进行降维的时候，
    第二种方法(Z-score standardization)表现更好。
    
    2） 在不涉及距离度量、协方差计算、数据不符合正太分布的时候，可以使用第一种方法或其他归一化方法。
    比如图像处理中，将RGB图像转换为灰度图像后将其值限定在[0 255]的范围。


#### 常见的激活函数，及其优缺点
* sigmod函数

* tanh函数

* ReLu函数

* ELU函数

* PReLu函数

* swish函数

#### 梯度消失和梯度膨胀的原因及其解决方法
[博客](https://blog.csdn.net/donkey_1993/article/details/81807847?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-1.edu_weight)
#### xgboost和GDBT的区别

#### 导致overfitting的原因及其解决方法