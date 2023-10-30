---
title: Latex-Beamer快速入门
date: 2023-09-08
category: [Technology,LaTex]
toc_number: false
---

官方教程: [The beamer class User Guide for version 3.70.](http://tug.ctan.org/macros/latex/contrib/beamer/doc/beameruserguide.pdf) （最新版）

安装好Texlive后可以在命令行中使用`texdoc beamer`打开安装版本的官方文档。

参考文章：

[知乎-如何使用beamer制作学术会议、学术演讲的幻灯片slides?](https://zhuanlan.zhihu.com/p/266399513)
[知乎-Beamer教程](https://zhuanlan.zhihu.com/p/584431029)

# 0 Prerequisite
需要首先在本机配置好Latex环境，beamer支持pdflatex, latex+dvips, lualatex, xelatex.

# 1 Configurations
## 1.1 document class
```Latex
\documentclass{ctexbeamer} % 中文使用ctexbeamer
\documentclass{beamer}     % 纯英文使用beamer
```
## 1.2 theme
使用usetheme来应用主题，同时可以通过template自定义配置
```Latex
\usetheme{}
\setbeamertemplate{footline}[FootlineTemplateII] % 底部增加一行
```
主题查看页面：[theme-matrix](https://hartwork.org/beamer-theme-matrix/)

STFI for more themes!

## 1.3 infos
和article中一样，beamer中幻灯片的标题、作者、日期等信息都可以在导言区以相同方式书写
```Latex
\title{...}
\author{...}
\date{\today}
\logo{\includegraphics[height=1.5cm]{logo.jpg}} % 默认logo加在右下角
```

## 1.4 catalogue
### 1.4.1 整体目录
```Latex
\begin{frame}{catalogue}
\tableofcontents     % 生成目录
\end{frame}
```

### 1.4.2 小节前导目录
在导言区加上以下代码可以生成每一小节前的前导目录
```Latex
\AtBeginSection[]
{
  \begin{frame}
    \frametitle{Table of Contents}
    \tableofcontents[currentsection]
  \end{frame}
}
```

## 1.5 font
### 1.5.1 全局
- **大小**：可以在`\documentclass[10pt]{beamer}`的方括号中修改字体大小
- **字体**：
  1. 使用字体主题`\usefonttheme{...}`, 可用字体包括：structurebold, structurebolditalic, structuresmallcapsserif, structureitalicsserif, serif 以及 default
  2. 通过引入相应的包来设置：mathptmx, helvet, avat, bookman, chancery, charter, culer, mathtime, mathptm, newcent, palatino, pifont and utopia
   
### 1.5.2 局部
设置局部字体格式可以在导言区使用`\setbeamerfont{structure}{size={\fontsize{6pt}{0pt}}}`

## 1.6 color
color和主题强相关，对于某一项主题，可以使用`\usecolortheme{...}`来配置。

可以引入xcolor包使得颜色更丰富。

# 2 Contents
在导言区配置完后，所有的内容都包括在：
```Latex
\begin{document}
...
\end{document}
```

## 2.1 Sections
beamer和article一样，使用section来划分章节。beamer可以根据section自动生成目录页插入。
```Latex
\section{}
\subsection{}
\section*{} % 无编号章节
```
一个section中可以包含多个subsection，每个section/subsection可以包含多个幻灯片页面。

## 2.2 Frames 
beamer中，frame包含了页面部分
```Latex
\begin{frame}
    \titlepage  % 显示标题页面
    \tableofcontents % 显示目录页面
\end{frame}
```

## 2.3 Alert
使用`\alert{...}`来强调文字，文字会自动标红

## 2.4 Block
在页面上以块的方式展示

```Latex
\begin{block}{Remark} % block title
...
\end{block}

\begin{alertblock}{Important theorem}
Sample text in red box % block content
\end{alertblock}
```
## 2.5 Graphs
插入图片需要graphix宏包
```Latex
\begin{figure}[ht]
    \centering
    \includegraphics[width=0.8\textwidth]{dataset.png}
    \caption{A picture downloaded from the Internet.png} % 图片下方文字说明
    \label{dataset}
\end{figure}
```

## 2.6 Multiple Columns
```Latex
\begin{columns}
    \column{0.5\textwidth}
    This is a text in first column.
    $$E=mc^2$$

    \column{0.5\textwidth}
    This text will be in the second column
    and on a second tought this is a nice looking
    layout in some cases.
\end{columns}
```
使用columns来呈现分栏效果