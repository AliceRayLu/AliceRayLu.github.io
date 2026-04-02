---
title: vscode使用github copilot问题
date: 2026-03-31
category: [Technology,Device Usage]
toc_number: false
---

## 本地以及wsl copilot无法连接
安装copilot插件后，在win环境中可以正常使用，但是在wsl中连不上，即使配置了wsl代理也没有用。STFI之后，参考这篇博客，https://www.cnblogs.com/o2iginal/p/17800963.html （github上的issue也没有解决这个问题）但是当给vscode设置代理后，就可以使用了。

vscode settings -> search 'proxy' -> http代理地址设置为本地代理的地址（我的机器上是clash地址）

然后reload vscode window，就可以正常使用了。

## 远程copilot无法连接

最近经常出现远程的机器代理服务不稳定问题，有以下解决方案：

- 让插件运行在本地，打开设置，搜索extension kind，编辑settings文件

```json
"remote.extensionKind": {
    "Github.copilot-chat":[
        "ui"
    ]
}
```