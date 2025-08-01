---
title: Transformer Learning Materials
date: 2024-09-29
category: [LLM]
toc_number: false
---

## 1 前置知识-Encoder&Decoder结构

encoder和decoder是一种模型结构，并不是某一个特定的神经网络模型。整体部分分为encoder编码器，decoder解码器：

- encoder编码器：将文字、图片、音视频转换为向量
- decoder解码器：将向量翻译/恢复为文字、图片、音视频

我们所熟悉的CNN、RNN、LSTM就可以用来充当encoder、decoder部分。

这个结构必须保证，encoder和decoder之间使用的向量维度是相同且固定的

