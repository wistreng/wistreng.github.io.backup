---
layout: post
title: Basic Statistic Terms
key: 20171005
tags: Statistic Mathematic
---

Given a set of n samples $$x=\{x_1,\ldots,x_n\}$$

1. **Arithmetic mean value**
    $$\bar x={\sum x_i \over N}$$
<!--more-->
2. **Geometric mean**
$$x=^n\sqrt {\prod_{i=1}^N x_i}$$
3. **Root mean square average**
$$x_{rms}=\sqrt  {{1\over N}\sum_{i=1}^N x_i^2}$$
4. **harmonic mean**
$$x = {N\over \sum_{i=1}^N {1\over x_i}}$$
5. **Weighted average**
$$\bar x = {\sum_{i=1}^N w_ix_i \over \sum_{i=1}^N w_i}$$
6. **Variance**
$$S^2={\sum (x_i-\bar x)^2 \over N}$$
7. **Standard Deviation**
$$S=\sqrt{\sum (x_i-\bar x)^2 \over N}$$
8. **Covariance**
$$cov(X,Y)=\frac{\sum_{i=1}^n (X_{i}-\bar{X})(Y_{i}-\bar{Y})}{n-1}$$
9. **Covariance matrix**
When it comes to n>2 dimension, the data set need to calculate $$\frac{n!}{(n-2)!*2}$$ Covariances, then we use a Matrix to organize these cov, so the definition of covariance matrix is:
$$C_{n\times n}=(c_{i,j},c_{i,j}=cov(Dim_{i},Dim_{j}))$$
For example, a data set have $$\{x,y,z\}$$ three dimension, its cov matrix is:
![Cov Matrix](http://7jptbo.com1.z0.glb.clouddn.com/images/covariance-1.jpg"Cov Matrix")