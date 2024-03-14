---
title: 24 Summer Intern 面试记录
date: 2024-01-14
category: Stories
---

# Timeline
|公司/职位/base                        | 投递时间  | 通知时间 | 一面时间 | 二面时间 | offer |
|    :--                              |   :--:    |   :--:  |  :--:   | :--:    | :--: |
|Google / SE summer intern / Shanghai | 12.16 |12.19（补充学历成绩等信息，面试时间）12.26（收到recruiter邮件）|1.15| 1.17 | 1.24挂 |
|Microsoft / SWE intern / Shanghai or Beijing |2.2 |2.14（填写问卷） |     |    |    |
|vivo / frontend intern / Nanjing     | 2.21  |  2.25（填写测评） |        |         |          |
|美团 / 前端实习 / Shanghai or Beijing | 2.26 | 3.8（参与3.9笔试） |         |         |         |
|网易雷火 / web前端实习 / Hangzhou    |  2.27   |       |    |    |      |
|腾讯 / web前端 / ？    | 2.28  |   3.11（腾讯云捞起来）    |  3.12  |      |      |
|Morgan Stanley/ IT技术部实习 / Shanghai | 2.29 | 3.1（fast track预约面试时间）3.8（online assessment） | 3.6电面 |      |      |
|Mihoyo / 前端 / Shanghai     | 2.29 |      |      |       |           |
|小米 / 前端开发 / Nanjing            | 3.4 |   |     |     |       |
|拼多多 / 前端 / Shanghai             | 3.4 |  |    |   |   |
|京东 / 前端 / Shanghai or Beijing    | 3.4 |   |    |     |     |
|携程 / 前端 / Shanghai               | 3.4 | 3.11（3.13笔试）|    |     |     |
|蚂蚁 / 前端(支付宝) / Shanghai       | 3.8  |  3.14简历挂   |    |     |     |
|恒生 / 前端 / Hangzhou               | 3.8  |    |    |     |     |



# 信息来源
大部分企业都会在官方“xx招聘”公众号上发布暑期实习的相关内容，对于国内的一些企业辅导员或校方也会发布信息，及时关注这些信息，注意截止的一些时间点，越早投递越好。

# 简历内容
个人简历是23暑期就准备好的，内容：华五本+较高GPA以及排名+一些比赛/大作业项目+一些水奖项和奖学金。没有托福雅思，但是有较高（630+）四六级，尚不清楚英语水平是否在简历筛选范围内。

# Google
google一般都是最早开始暑期实习招聘的，2023年是12月14号开始暑期实习的招聘的。我通过关注官方微信公众号"google招聘包打听"看到的职位信息，因此很早就开始投递了。同时本人没有找内推，在等待面试通知时花了较长时间，一度以为简历就挂了（也有可能外企要放圣诞假期？）。总之收到recruiter邮件时还是很开心的。

一面二面都是45min，在google meet里面视频，另外开一个google doc类似于共享文档的记事本写代码。

## Google一面
英文面，上来先是打印二叉树，需要打印成"human can understand"。。。然后在那边空格对齐写了老半天，感觉浪费了太多的时间。

第二题是数组里面找出最大的奇数，变形题是找到第k大的奇数。直接回答了一下用堆，由于二叉树写太久了没来得及写完堆。

## Google二面
中文面，又是类似二叉树，把一个字符串分到了各个叶子节点，父节点保存子节点的长度和。第一个问题让设计了一个结构来表示这个树，我定义了一个结构体同时保存string和len。没有想出可以在父节点不用string来节省空间的方法，后来想想也许用继承？（很久没有用c++写面向对象了）

第二个问题是查询字符串中第k个字符所在的位置。这个按照传统的递归做法即可。然后需要自己设计测试用例，考虑一些边界情况，来验证和修改自己的代码。最后是说一下自己写的时间复杂度和空间复杂度。

整体感觉难度好像还行，没有想象中那么难，但是让我写打印二叉树是属实没有想到的，大概率最后挂是挂在了一面，写打印二叉树花了太久的时间在计算对齐的空格个数上，还是学艺不精吧 :==(

# Microsoft

# vivo


# Morgan Stanley

## 电面

涉及的方面比较多，包括c++，Java，OS，DB以及数据结构。但是内容相对固定，就是传统的一些问题。算法题刚好问到了数据流的中位数，前两天刚做过印象深刻。（主要是看微软面经看到了这道题，就去做了一下，没想到外企题库出奇地一致啊）

internet: TCP/UDP
c++：stack/heap，abstract class (example), smart pointer
java：garbage collection(advantage / disadvantage)
os：process/threads, dead lock, starving
db: index, primary key, foreign key, inner/outer join
Algorithm：linked list(head node), BST, time complexity of operations 

# 美团

## 笔试
实习生笔试分为两部分，一部分是选择题，包括很多基础知识，数据库、编译原理、os、计组、设计模式以及一些数学题，主要是找规律和鸡兔同笼类似的简单计算题。

另一部分是两道easy级别的算法题，没想到算法题那么简单，一个小时就提交了前面的选择题，不能回去改了，早知道多花点时间好好考虑选择题了呜呜。