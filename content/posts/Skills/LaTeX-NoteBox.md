---
title: "在LaTeX中加入标注与引用块"
date: 2025-02-04T21:31:21+08:00
lastmod: 2025-02-04T21:31:21+08:00
author: ["Glacier"]

categories:

tags:
- LaTeX
- tcolorbox

keywords:
- word 1
- word 2

description: "" # 文章描述，与搜索优化相关
summary: "" # 文章简单描述，会展示在主页
weight: # 输入1可以顶置文章，用来给文章展示排序，不填就默认按时间排序
slug: ""
draft: false # 是否为草稿
comments: true
showToc: true # 显示目录
TocOpen: true # 自动展开目录
autonumbering: true # 目录自动编号
hidemeta: false # 是否隐藏文章的元信息，如发布日期、作者等
disableShare: true # 底部不显示分享栏
searchHidden: false # 该页面可以被搜索到
showbreadcrumbs: true #顶部显示当前路径
mermaid: true
cover:
    image: ""
    caption: ""
    alt: ""
    relative: false
---
以Obsidian为例，当我们希望在其中实现标注或者引用块时，我们可以借助以下代码实现
```Markdown
>[!info]
>一个标注

>一条引用

```
效果如下
[![image.png](https://i.postimg.cc/Kjdcv2C4/image.png)](https://postimg.cc/H891BfYC)
在$\LaTeX$中，通过```tcolorbox```宏的帮助，我们也可以实现类似的效果
下附代码与使用样例
```LaTeX
\documentclass{article}
\usepackage{ctex}
\usepackage{fontawesome5}
\usepackage[most]{tcolorbox}
\newtcolorbox[]{infobox}[1][] % 定义名为 infobox 的环境
{enhanced,                    % 启用增强模式
	colback = blue!10,         % 主背景色：10% 蓝色
	toptitle= 2mm,
	colbacktitle = blue!10,    % 标题背景色：同主背景
	coltitle = black,          % 标题文字颜色：黑色
	boxrule = 0pt,             %隐藏标题和正文间的空隙
	frame hidden,              % 隐藏边框
	fonttitle = \bfseries\sffamily, % 标题字体：加粗无衬线
	breakable,                 % 允许跨页分断
	before skip = 3ex,         % 环境前间距：3ex
	after skip = 3ex,          % 环境后间距：3ex
	title={\faInfoCircle\hspace*{0.5mm} Info},                % 标题内容
	label=#1                   % 可选的引用标签
}
% 定义名为 citebox 的环境
\newtcolorbox[]{citebox}[1][] 
{
	enhanced,                    % 启用增强模式（允许更复杂的样式设置）
	coltitle = black,           % 标题文字颜色（当前未使用标题）
	boxrule = 0pt,              % 边框线宽度设为 0（隐藏默认边框）
	frame hidden,               % 隐藏外框架（与 boxrule=0pt 效果叠加）
	borderline west = {0.5mm}{0.0mm}{black}, % 左侧装饰线（宽度/偏移/颜色）
	fonttitle = \bfseries\sffamily, % 标题字体设置为加粗无衬线（若使用标题时生效）
	breakable,                  % 允许跨页分割（长内容可自动分页）
	before skip = 3ex,          % 环境前的垂直间距（3倍字母x高度）
	after skip = 3ex,           % 环境后的垂直间距
	label= #1                          % 允许输入标签作为第一个参数
}

\begin{document}
	% 标注块效果
	\begin{infobox}[1]
		这是一个 `info` 类型的标注块，类似于 Obsidian 里的 `[!info]`。
	\end{infobox}

% 引用块效果
	\begin{citebox}
	引用文本

	\end{citebox}
\end{document}
```
效果图
[![LaTeX.png](https://i.postimg.cc/D0gZ6DNz/LaTeX.png)](https://postimg.cc/RJW4VP4r)

如果对颜色不满意，可以更改设定中的颜色数值，更复杂的颜色配置可借助宏```xcolor```实现
<!-- more -->
