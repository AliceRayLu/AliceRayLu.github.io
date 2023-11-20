---
title: Latex快速入门/速查
date: 2023-08-04
category: [Technology,LaTex]
toc_number: false
---


详细文档参考（以下文档不包含安装教程）

🔗**https://liam.page/2014/09/08/latex-introduction/**

## 1 工具安装与环境配置

TeX live + vscode （某乎有详细教程）

## 2 排版工具与编译模式

pdfTeX, pdfLaTeX, XeTeX, XeLaTeX

> Note：文档使用中文可以使用ctex包+XeLaTex编译！！！<mark>代码：`\usepackage{ctex}`</mark>

## 3 语法

```LaTeX
\documentclass[UTF8]{article}
% 导言区
\begin{document}
Hello, world!
\end{document}
```

 **控制序列：** 控制序列是latex的核心语法，`{...}`表示参数，`[]`表示可选参数

### 3.1 注释

以`%`作为注释标记，当前行直到末尾全部为注释

**【注意】**输出%字符本身需要加`\`转义，这与latex中的特殊字符有关。经常会使用到的`_`下划线字符在文字内容中不能直接使用，
需要用`\_`来表示，否则会与latex自身系统默认功能冲突从而引发报错！

### 3.2 文本环境

控制序列`\begin{...}`和`\end{...}`成对出现，必须保证二者{}中的参数一致

两个控制序列中间的内容被称为**环境**

只有在document环境中的内容才会被正常输出到文档中（即`\end{document}`之后插入任何内容都是无效的）

### 3.3 导言

从 `\documentclass{article}`开始到 `\begin{document}` 之前的部分被称为导言区

导言区进行对整篇文章的格式设置

【一些配置选项】

```LaTeX
\title{你好，world!}
\author{Liam}
\date{\today}
```

【 **宏包** 】

由于某些控制序列较为常用，所以打包到一个文件中，每次只需要在导言区直接调用

语法：`\usepackage{}`

常用`\usepackage{ctex}`使得文档支持中文(`ctex`需要使用`XeLaTex`编译)

 **【标题】** 在正文中使用maketitle使得标题展示在文档中

```LaTeX
\title{hihihi}
\begin{document}
\maketitle
\end{document}
```

### 3.4 章节与段落

* `\section{}`
* `\subsection{}`
* `\subsubsection{}`
* `\paragraph{}`
* `\subparagraph{}`

### 3.5 列表

无序列表

```LaTeX
\begin{itemize}
\item ...
\end{itemize}
```

有序列表（中括号可以修改列表编号形式）
```LaTeX
\begin{enumerate}
\item[1.]
\end{enumerate}
```

### 3.6 目录

在`\maketitle`下一行写`\tableofcontents`自动生成目录

### 3.7 数学公式

**注意**：当数学公式编译出现`undefined`情形时，需要注意是否引入了数学相关的包，比如`amsmath`等。

#### 3.7.1 模式

* 行内模式：使用`$...$`插入行内公式（或者`\(...\)`也可以实现行内公式）  
  【注】使用  $$来显示公式使用了plainTex风格，会改变默认行间距，不推荐
* 行间公式：使用`\[...\]`插入行间公式
* 公式编号：

  ```LaTeX
  \begin{equation}
  ...
  \end{equation}
  ```
  使用`equation*`可以取消公式编号

#### 3.7.2 上下标

* 上标 `^`
* 下标 `_`

所有上下标默认只作用于之后紧跟的一个字符，使用`{}`来包括多个字符

文章中非数学公式的上下标（<mark>文字角标</mark>）可以使用`\textsuperscript{}`表示上标，`\textsubscript{}`表示下标

#### 3.7.3 根式和分式

```LaTeX
\sqrt{x}    %表示根号x
\frac{1}{2} %表示1/2
```

如果要强制行内模式的分式显示为行间模式的大小，可以使用 `\dfrac`, 反之可以使用 `\tfrac`

#### 3.7.4 对齐

使用aligned环境

```LaTeX
\begin{aligned}
...
\end{aligned}
```

补充：

* 可以使用`\\`结合`&`使得公式换行对齐，`\\`写在行结尾，`&`写在行开头
* `\\`用于普通文本换行
* `\par`是带有缩进的换行，两行输入文本之间隔一行会自动缩进换行，输入文本之间无`\\`符号会自动连续

#### 3.7.5 公式组

* 使用gather环境，默认不对齐：`\begin{gather}...\end{gether}`
* 使用align环境对齐公式组：`\begin{align}...\end{align}`

#### 3.7.6 导数

* 偏导 $\frac{\partial f}{\partial x}$

  ```LaTeX
  \frac{\partial f}{\partial x}
  ```
* 求导 $\frac{\mathrm{d} y}{\mathrm{d} x}$

  ```LaTeX
  \frac{\mathrm{d} y}{\mathrm{d} x}
  ```
* 拉普拉斯 梯度 $\nabla$

  ```LaTeX
  \nabla f
  ```

#### 3.7.7 特殊字体
花体包（Scripts）：`mathrsfs`

```LaTeX
$\mathscr{A}$
```
注：这个花体包似乎不支持小写字母。

#### 总结

数学公式的具体使用请参看

**https://katex.org/docs/supported.html**

### 3.8 插入图片

#### 3.8.1 法一

使用`graphicx`宏包提供的`\includegraphics`命令，文件要在.tex文件同目录下

```LaTeX
\begin{document}
\includegraphics[width = .8\textwidth]{a.jpg} %插入a.jpg文件
\end{document}
```

`[width = .8\textwidth]`将图片缩放到页面宽度的80%

#### 3.8.2 法二
```LaTex
\begin{figure}
\includegraphics[width = .8\textwidth]{a.jpg}
\end{figure}
```

### 3.9 插入表格

使用`tabular`环境

```LaTeX
\begin{tabular}{|l|c|r|}
 \hline
操作系统& 发行版& 编辑器\\
 \hline
Windows & MikTeX & TexMakerX \\
 \hline
Unix/Linux & teTeX & Kile \\
 \hline
Mac OS & MacTeX & TeXShop \\
 \hline
通用& TeX Live & TeXworks \\
 \hline
\end{tabular}
```

* `\hline` 命令表示横线
* 在列格式中用 `|` 表示竖线
* 用 `&` 来分列，用 `\\` 来换行；
* 每列可以采用居左、居中、居右等横向对齐方式，分别用 `l`、`c`、`r` 来表示。

有关表格的详细使用请查看[这篇博客](https://blog.csdn.net/xovee/article/details/109254872)

使用`\begin{table}`包裹tabular可以实现居中、浮动、添加说明等操作

### 3.10 浮动体

关于浮动体的研究待补充...

### 3.11 字体处理

#### 3.11.1 斜体

使用`\emph`或者`\textit`命令

`\emph`主要用来显示强调文字

> `\emph`命令的实际行为取决于它所处的环境，在正常文本中，它会让文字变成斜体，而如果在斜体文字中，它会让文字变成正常。
>

#### 3.11.2 粗体

使用`\textbf`

#### 3.11.3 下划线

使用`\underline`

#### 3.11.4 加粗+斜体

```LaTeX
\textbf{\textit{accident}}
```

#### 3.11.5 文本边框

```LaTeX
\fbox{}
\framebox[<宽度>][<位置>]{...}
```

```LaTeX
\setlength{\fboxrule}{0.4pt}  \fbox{内容} %调整边框粗细
\setlength{\fboxsep}{1em}   \fbox{内容} %调整文字内边距
```
