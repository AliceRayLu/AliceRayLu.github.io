---
title: Umich EECS 498-007
date: 2023-10-30
category: [Knowledge, Machine Learning]
toc_number: false
---

课程主页：🔗https://web.eecs.umich.edu/~justincj/teaching/eecs498/WI2022/

在课程主页可以找到2019年的youtube课程录屏以及6项hw/Assignments。通过google colab打开完成作业。

这篇博客记录一些课堂笔记和作业笔记。可以在[这个仓库]()中找到本人的作业实现

> 正在施工建设中......

## Lec 2: Image Classification
常用数据集：
- **CIFAR-10** & **CIFAR-100**
    图像尺寸：32*32
    CIFAR-10有10类图像，每类6000张。总共分为50000张训练图片和10000张测试图片。
    CIFAR-100有100类图像，每类600张，包括500张训练图片和100张测试图片。
- **ImageNet**
    最著名图像数据集，有1000类图像分类，数据量较大，有miniImageNet
- **MNIST**
    手写数字图像集
    图像尺寸：28*28
    50000张训练图片，10000张测试图片

## A1: Pytorch & KNN
### Pytorch 101
#### 1 Tensor Basic
创建tensor使用python数组形式

```py
import torch

a = torch.tensor([[0,1,2],[3,4,5]])
print(a.dim())
print(a.shape)
print(a.size())
print(a[1,1])
```
输出结果
> 2
> torch.Size([2,3])
> torch.Size([2,3])
> 4

`shape`是属性，`size()`是方法，返回的结果相同，可以使用`shape[1]`获取具体某一个维度大小

#### 2 Tensor Index
