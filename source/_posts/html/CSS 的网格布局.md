---
title: CSS 的网格布局
tags: [前端,html,css]
date: 2025-10-24 08:08:08
---

# [#](#f46ffd)[CSS 的网格布局](https://xplanc.org/primers/document/zh/03.HTML/02.%E6%A0%B7%E5%BC%8F/09.%E7%BD%91%E6%A0%BC%E5%B8%83%E5%B1%80.md#f46ffd)

CSS 网格布局（Grid Layout）是一个强大的 2D 布局系统，可精确地控制页面的行和列布局，比 Flex 更适合结构化排布。

通过将一个元素样式的 `display` 属性设为 `grid`，可以将该元素设为网格布局的 **容器**。

通过容器的 [`grid-template-columns`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.template.md) 属性可以配置网格的列宽度，通过 [`grid-template-rows`](https://xplanc.org/primers/document/zh/03.HTML/EX.HTML%20%E5%85%83%E7%B4%A0/EX.template.md) 属性可以配置网络的行高度。

下面这个示例将网格设为二行四列，两行的高度分别为 40px 和 80px，四列的宽度分别为 40px，80px，120px 和 160px。

```html
<!-- 网格有四列，宽度依次为 40px 80px 120px 160px -->
<!-- 网格有两行，高度依次为 40px 80px-->
<div style="display:grid; grid-template-columns:40px 80px 120px 160px; grid-template-rows:40px 80px;">
    <div style="background-color:red;"></div>
    <div style="background-color:yellow;"></div>
    <div style="background-color:blue;"></div>
    <div style="background-color:orange;"></div>
    <div style="background-color:green;"></div>
    <div style="background-color:purple;"></div>
    <div style="background-color:cyan;"></div>
    <div style="background-color:pink;"></div>
</div>

```

display:grid
    

## [#](#47c6db)[单位 fr](https://xplanc.org/primers/document/zh/03.HTML/02.%E6%A0%B7%E5%BC%8F/09.%E7%BD%91%E6%A0%BC%E5%B8%83%E5%B1%80.md#47c6db)

可以使用特殊的单位 `fr` 按比例分配列的宽度（或行的高度）。

下面这个示例将网格设为二行四列，两行的高度分均 40px，四列的宽度为 。

```html
<!-- 网格有四列，宽度为 1:2:2:1 -->
<!-- 网格有两行，高度依次为 40px 40px-->
<div style="display:grid; grid-template-columns:1fr 2fr 2fr 1fr;grid-template-rows:40px 40px;">
    <div style="background-color:red;"></div>
    <div style="background-color:yellow;"></div>
    <div style="background-color:blue;"></div>
    <div style="background-color:orange;"></div>
    <div style="background-color:green;"></div>
    <div style="background-color:purple;"></div>
    <div style="background-color:cyan;"></div>
    <div style="background-color:pink;"></div>
</div>

```

grid-template-columns:1fr 2fr 2fr 1fr
    

## [#](#25e2b6)[repeat](https://xplanc.org/primers/document/zh/03.HTML/02.%E6%A0%B7%E5%BC%8F/09.%E7%BD%91%E6%A0%BC%E5%B8%83%E5%B1%80.md#25e2b6)

可以使用 `repeat` 函数简化代码。

```css
repeat(重复次数, 被重复的值)

```

下面这个示例将网格设为二行四列，两行的高度分均 40px，四列的宽度为 。

```html
<!-- 网格有四列，宽度相同 -->
<!-- 网格有两行，高度均为 40px -->
<div style="display:grid; grid-template-columns:repeat(4, 1fr);grid-template-rows:repeat(2, 40px);">
    <div style="background-color:red;"></div>
    <div style="background-color:yellow;"></div>
    <div style="background-color:blue;"></div>
    <div style="background-color:orange;"></div>
    <div style="background-color:green;"></div>
    <div style="background-color:purple;"></div>
    <div style="background-color:cyan;"></div>
    <div style="background-color:pink;"></div>
</div>

```

grid-template-columns:repeat(4, 1fr)
    

## [#](#b27bf1)[minmax](https://xplanc.org/primers/document/zh/03.HTML/02.%E6%A0%B7%E5%BC%8F/09.%E7%BD%91%E6%A0%BC%E5%B8%83%E5%B1%80.md#b27bf1)

可以使用 `minmax` 函数设置单元格宽度的最小值和最大值，通常与 `repeat` 搭配，适用于响应式设计。

```css
repeat(重复次数, minmax(最小宽度, 最大宽度))

```

重复次数通常使用 `auto-fill` 和 `auto-fit`：

* `auto-fill` 满足宽度的前提下，单元格数量尽可能多
* `auto-fit` 满足宽度的前提下，填满行

下面的示例中，容器的宽度在不断变化。网格将自动适应容器的宽度，列宽最小不小于 `100px`。

可以看到 `auto-fit` 模式下，当容器宽度不小于 `500px` 时，由于只包含了 4 个单元，因此最多只被划分为 4 列；单元格的宽度被拉伸。

而 `auto-fill` 模式下，当容器宽度不小于 `500px` 时，尽管只包含了 4 个单元，网格仍被划分为了更多列；单元格仅占据相应的列。

```html
<!-- 单元格宽度最小 100px，最大 1fr（无限），自动填满行宽度 -->
<!-- 单元格高度为 40px -->
<div style="display:grid; grid-template-columns:repeat(auto-fit, minmax(100px, 1fr));grid-template-rows:repeat(auto-fit, 40px);">
    <div style="background-color:red;"></div>
    <div style="background-color:yellow;"></div>
    <div style="background-color:blue;"></div>
    <div style="background-color:orange;"></div>
</div>

<!-- 单元格宽度最小 100px，最大 1fr（无限），自动填满行宽度 -->
<!-- 单元格高度为 40px -->
<div style="display:grid; grid-template-columns:repeat(auto-fill, minmax(100px, 1fr));grid-template-rows:repeat(auto-fit, 40px);">
    <div style="background-color:red;"></div>
    <div style="background-color:yellow;"></div>
    <div style="background-color:blue;"></div>
    <div style="background-color:orange;"></div>
</div>

```

响应式网格布局 auto-fit


响应式网格布局 auto-fill


> 上例中，单元格的最小宽度是 100px，最大宽度是无限。当网格容器的宽度为 500px 时， 若 ，则单元格宽度小于 100px 不满足宽度要求。因此  。
> 
> * `auto-fill` 倾向于单元格更多，因此列数为 5，单元格宽度为 100px，四个元素占前四列。
> * `auto-fit` 倾向填满行，由于子元素数量只有四个，因此列数为4，单元格宽度为 125px。

---

> 《[CSS 的网格布局](https://xplanc.online/2baabc72c8b0dc2c143397929c7e968b014ac7ae92a04d6113407c3c51aeeca8)》 是转载文章，[点击查看原文](https://xplanc.org/primers/document/zh/03.HTML/02.%E6%A0%B7%E5%BC%8F/09.%E7%BD%91%E6%A0%BC%E5%B8%83%E5%B1%80.md)。