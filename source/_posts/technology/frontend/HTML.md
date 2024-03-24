---
title: 【前端八股】HTML
date: 2024-03-09
category: [Technology,Frontend]
toc_number: false
---

# 1 HTML5新特性

# 2 语义化标签

# 3 块级元素与行内元素

## 3.1 块级元素
- div：容器
- dl：html5之前用于定义列表，与`<dt>`（子条目标题）和`<dd>`（子条目内容）嵌套使用
    ```html
    <dl>
        <dt>Beast of Bodmin</dt>
        <dd>A large feline inhabiting Bodmin Moor.</dd>

        <dt>Morgawr</dt>
        <dd>A sea serpent.</dd>
    </dl>
    ```
- form 
- h1 h2 h3 h4 h5 h6 
- hr 
- ol li p pre table td tr

## 3.2 行内元素

a b s i u span br img input textarea sub sup

## 3.3 行内与块级元素的区别

行内元素：
1. 无法设置宽高；
2. 对margin仅设置左右有效，上下无效；
3. padding上下左右有效；不会自动换行

块级元素：
1. 可以设置宽高
2. margin和padding的上下左右均对其有效
3. 超出当前行会自动换行
4. 多个块状元素标签写在一起，默认排列方式为从上至下

# 4 标签中嵌入
使用`&lt;`在标签中使用尖角符号
```html
<p> 这是被&lt;p&gt;包含起来的内容</p>
```