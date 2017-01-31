---
layout: post
title: markdown语法
categories: 技术教程
tags: [标记语言, 语法]
comments: true
---

#相关教程
[Cmd Markdown 高阶语法手册 - 作业部落](https://www.zybuluo.com/mdeditor?url=https%3A%2F%2Fwww.zybuluo.com%2Fstatic%2Feditor%2Fmd-help.markdown)
[Markdown语法介绍 - Coding](https://coding.net/help/doc/project/markdown.html)
[Markdown - 维基百科，自由的百科全书](https://zh.wikipedia.org/wiki/Markdown)
[Markdown 语法说明(简体中文版) - Wow! Ubuntu](http://wowubuntu.com/markdown/)
[Markdown 语法说明 (简体中文版)](https://github.com/riku/Markdown-Syntax-CN/blob/master/syntax.md)
[Cmd Markdown 公式指导手册](https://www.zybuluo.com/codeep/note/163962)

#语法介绍
###斜体与粗体
使用 * 和 ** 表示斜体和粗体。
示例：
这是 *斜体*，这是 **粗体**。

###分级标题
你也可以选择在行首加井号表示不同级别的标题 (H1-H6)，例如：# H1, ## H2, ### H3，#### H4。

###分割线
你可以在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格。下面每种写法都可以建立分隔线：

----


###外链接
使用 \[描述](链接地址) 为文字增加外链接。
示例：
```
[本人博客](http://liuqinh2s.com)
```
这是去往 [本人博客](http://teasion.github.io/blog) 的链接。
或者你也可以这样写：（引用的写法）

[本人博客][a link]

[a link]: http://liuqinh2s.com

```
[本人博客][a link]
[a link]: http://liuqinh2s.com
//只要文本中有这一行就行，这样写是为了把链接和脚注等都放到一起（一般放在文本最后）
```




###插入图像
使用 \!\[描述](图片链接地址) 插入图像。
示例：
![myGithubAvatar.png](https://ooo.0o0.ooo/2016/12/03/58429e1f4062b.png)
或者同样采用引用的写法
```
![Alt Image Text][image-id]
[image-id]: https://ooo.0o0.ooo/2016/12/03/58429e1f4062b.png "Optional Title"
```
![Alt Image Text][image-id]
[image-id]: https://ooo.0o0.ooo/2016/12/03/58429e1f4062b.png "Optional Title"

###无序列表

使用 `*，+，-` 表示无序列表。

示例：
- 无序列表项 一
- 无序列表项 二
- 无序列表项 三

### 有序列表
使用数字和点表示有序列表。
示例：
1. 有序列表项 一
2. 有序列表项 二
3. 有序列表项 三

### 文字引用
使用 > 表示文字引用。
示例：
> 野火烧不尽
> > 春风吹又生
> > >白居易

### 行内代码
使用
\`这里输入代码\`
`eval()`

### 代码块
使用
\`\`\`
这里输入代码
\`\`\`

```
#include <iostream>
```
###目录
使用\[toc\]
[toc]

###删除线
使用 ~~ 表示删除线。
~~这是一段错误的文本。~~

###注脚
使用 [^keyword] 表示注脚。
这是一个注脚[^footnote1]的样例。
这是第二个注脚[^footnote2]的样例。
[^footnote1]: 这是第一个

[^footnote2]: 这是第二个

###LaTex公式
\$ 表示行内公式：
质能守恒方程可以用一个很简洁的方程式$\lim_{x \to 0} \sin x$来表达。
\$\$ 表示整行公式：
$$\sum_{i=1}^n a_i=0$$
$$f(x_1,x_x,\ldots,x_n) = x_1^2 + x_2^2 + \cdots + x_n^2 $$
$$\sum^{j-1}_{k=0}{\widehat{\gamma}_{kj} z_k}$$
访问 [MathJax](http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference) 参考更多使用方法。

###流程图
#### 示例
```flow
st=>start: Start:>https://www.zybuluo.com
io=>inputoutput: verification
op=>operation: Your Operation
cond=>condition: Yes or No?
sub=>subroutine: Your Subroutine
e=>end
st->io->op->cond
cond(yes)->e
cond(no)->sub->io
```
#### 更多语法参考：[流程图语法参考](http://adrai.github.io/flowchart.js/)

### 表格支持
| 项目 | 价格 | 数量 |
| -------- | -----: | :----: |
| 计算机 | \$1600 | 5 |
| 手机 | \$12 | 12 |
| 管线 | \$1 | 234 |

###HTML标签
Markdown 语法中嵌套 Html 标签，譬如，你可以用 Html 写一个纵跨两行的表格：
<table>
    <tr>
        <th rowspan="2">值班人员</th>
        <th>星期一</th>
        <th>星期二</th>
        <th>星期三</th>
    </tr>
    <tr>
        <td>李强</td>
        <td>张明</td>
        <td>王平</td>
    </tr>
</table>



#特别介绍
##转义字符
使用像C语言中的\来进行转义：
$\lim$
\$ \lim \$

##多加空格
有些时候，有些支持Markdown的编辑类软件中，Markdown渲染失败，多半原因可能是没有空格导致的
比如：\#中文，在\#和中文之间加上一个空格就好了。这个问题我在很多地方遇到过，比如：Atom的Markdown Preview插件（这是一个Core Package）。

##一个小建议
使用HTML或者LaTex，或者结合笔记类软件的富文本工具栏来实现一些在Markdown中不尽如人意的地方
