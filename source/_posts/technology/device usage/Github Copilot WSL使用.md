---
title: 解决wsl vscode界面无法使用github copilot问题
date: 2024-12-23
category: [Technology,Device Usage]
toc_number: false
---

参考这篇博客，https://www.cnblogs.com/o2iginal/p/17800963.html github上的issure也没有解决这个问题，但是当给vscode设置代理后，就可以使用了。

vscode settings -> search 'proxy' -> http代理地址设置为本地代理的地址（我的机器上是clash地址）

然后reload vscode window，就可以使用了。
