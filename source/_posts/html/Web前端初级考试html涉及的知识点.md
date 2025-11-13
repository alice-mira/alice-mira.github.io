---
title: Web前端初级考试html涉及的知识点
tags: [前端,html]
---

#### HTML 基础概念

HTML（超文本标记语言）是构建网页的核心技术，用于定义网页结构和内容。考试通常涵盖以下基础知识点：

* HTML 文档基本结构：`<!DOCTYPE>` 声明、[`<html>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.html.md)、[`<head>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.head.md)（包含 [`<title>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.title.md)、[`<meta>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.meta.md) 等）、[`<body>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.body.md)。
* 常用标签：段落 [`<p>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.p.md)、标题 [`<h1>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.h1.md)\-[`<h6>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.h6.md)、链接 [`<a href="">`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.a.md)、图像 [`<img src="" alt="">`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.img.md)、列表 [`<ul>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.ul.md)/[`<ol>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.ol.md)/[`<li>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.li.md)。
* 文本格式化标签：[`<strong>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.strong.md)、[`<em>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.em.md)、[`<br>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.br.md)、[`<hr>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.hr.md)。

#### 表单与输入控件

表单是用户交互的关键部分，涉及标签和属性：

* [`<form>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.form.md) 标签的 `action` 和 `method` 属性（GET/POST）。
* 输入控件：[`<input type="text">`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.input.md)、[`<input type="password">`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.input.md)、[`<input type="radio">`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.input.md)、[`<input type="checkbox">`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.input.md)、[`<input type="submit">`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.input.md)。
* 其他控件：[`<textarea>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.textarea.md)、[`<select>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.select.md) 和 [`<option>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.option.md) 下拉菜单。
* 表单属性：`required`、`placeholder`、`disabled`、`readonly`。

#### 表格与语义化标签

表格用于数据展示，语义化标签提升可读性：

* 表格结构：[`<table>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.table.md)、[`<tr>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.tr.md)（行）、[`<td>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.td.md)（单元格）、[`<th>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.th.md)（表头）、[`<caption>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.caption.md)。
* 合并单元格：`colspan` 和 `rowspan` 属性。
* HTML5 语义化标签：[`<header>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.header.md)、[`<footer>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.footer.md)、[`<nav>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.nav.md)、[`<article>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.article.md)、[`<section>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.section.md)、[`<aside>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.aside.md)。

#### 多媒体与嵌入内容

现代网页常包含多媒体元素：

* 音频与视频：[`<audio>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.audio.md) 和 [`<video>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.video.md) 标签，支持 `controls`、`autoplay` 等属性。
* 嵌入外部内容：[`<iframe>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.iframe.md) 用于嵌入其他网页或资源。

#### 全局属性与元信息

* 全局属性：`class`、`id`、[`style`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.style.md)、[`title`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.title.md)、[`data-*`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.data.md)（自定义数据属性）。
* 元信息：[`<meta>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.meta.md) 标签的 `charset`（如 UTF-8）、`viewport`（响应式设计）、`description`（SEO 优化）。

#### HTML5 新特性

考试可能涉及 HTML5 新增功能：

* 本地存储：`localStorage` 和 `sessionStorage` 的简单概念。
* 绘图：[`<canvas>`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.canvas.md) 基础用法。
* 地理定位：`navigator.geolocation` 的简要介绍。

以上知识点需结合实践练习，例如手动编写表单或表格代码，以加深理解。

---

本文是转载文章，[点击查看原文](https://blog.csdn.net/2301_81365247/article/details/153210042)。