---
title: PySpark Tutorial
date: 2024-08-04
category: [Knowledge, Data Science]
---

spark是大数据处理框架，包括Spark RDD、Spark SQL、 Spark Streaming，MLlib，GraphX几大部分，
通常用于处理各种大数据任务。Spark基于内存计算，可以极大提升计算速度。

# 1 Spark存储与数据


# 2 DataFrame

## 2.1 分区

dataframe的存储是允许分布在多台不同物理计算机上，可以通过定义partition来定义数据的分布方式

如果不定义，一般采用随机分布的方式

## 2.2 Spark-Pandas Guide

### 2.2.1 获取数据

```python
data = spark.read.json("file name")
```

### 2.2.2 

可以用pandas函数操作，也可以用sql语句查询