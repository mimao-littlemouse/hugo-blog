---
# 帖子的发布作者
author: mimao
# 帖子的标题
title: 初识Hugo
# 帖子的日期
date: 2023-07-06
# 帖子的描述
description: Get you into a state quickly
# 帖子的标签
tags:
  - hugo
  - markdown syntax
# 帖子分类
categories:
  - Blog
# 设置帖子的封面
# image: hugo-start_cover.jpg
# 需要展示 数学表达式 的时候 请将math设置为true
math: true
---

### 摘要
```
\<!--more--\>
```

<!--more-->

***

### 标题
```
#### title
```
#### title

***

### 引用
```
> quote
```
> quote

***

### 引脚
```
<cite>去看我的解释[^1]</cite>
[^1]: 我是引脚的解释
```
<cite>去看我的解释[^1]</cite>
[^1]: 我是引脚的解释

***

### 表格

   Name | Age
--------|------
  mimao | 23

| Italics   | Bold     | Code   |
| --------  | -------- | ------ |
| *italics* | **bold** | `code` |

      Name | Age
    --------|------
      mimao | 23

    | Italics   | Bold     | Code   |
    | --------  | -------- | ------ |
    | *italics* | **bold** | `code` |

***

### 代码块
#### \`\`\` 换行 代码块 \`\`\`
    ```html
    <!doctype html>
    <html lang="en">
    <head>
      <meta charset="utf-8">
      <title>Example HTML5 Document</title>
    </head>
    <body>
      <p>Test</p>
    </body>
    </html>
    ```

#### 用4个空格 形成的代码块

    <!doctype html>
    <html lang="en">
    <head>
      <meta charset="utf-8">
      <title>Example HTML5 Document</title>
    </head>
    <body>
      <p>Test</p>
    </body>
    </html>

#### 带有Hugo内部高亮短代码的代码块
    \{\{< highlight html >\}\}
    <!doctype html>
    <html lang="en">
    <head>
      <meta charset="utf-8">
      <title>Example HTML5 Document</title>
    </head>
    <body>
      <p>Test</p>
    </body>
    </html>
    \{\{< /highlight >\}\}

#### 代码改动对比 代码块（Diff code block）

    ```diff
    [dependencies.bevy]
    git = "https://github.com/bevyengine/bevy"
    rev = "11f52b8c72fc3a568e8bb4a4cd1f3eb025ac2e13"
    - features = ["dynamic"]
    + features = ["jpeg", "dynamic"]
    ```

```diff
[dependencies.bevy]
git = "https://github.com/bevyengine/bevy"
rev = "11f52b8c72fc3a568e8bb4a4cd1f3eb025ac2e13"
- features = ["dynamic"]
+ features = ["jpeg", "dynamic"]
```

***

### 列表

#### 有序列表

```
1. First item
2. Second item
3. Third item
```
1. First item
2. Second item
3. Third item

#### 无序列表

```
* List item
* Another item
* And another item
```
* List item
* Another item
* And another item

#### 嵌套列表

```
* Fruit
  * Apple
  * Orange
  * Banana
* Dairy
  * Milk
  * Cheese
```
* Fruit
  * Apple
  * Orange
  * Banana
* Dairy
  * Milk
  * Cheese

***

### 其他标签元素 — abbr, sub, sup, kbd, mark

#### abbr
    <abbr title="Graphics Interchange Format">GIF</abbr> is a bitmap image format.
<abbr title="Graphics Interchange Format">GIF</abbr> is a bitmap image format.

#### sub
    H<sub>2</sub>O
H<sub>2</sub>O

#### sup
    X<sup>n</sup> + Y<sup>n</sup> = Z<sup>n</sup>
X<sup>n</sup> + Y<sup>n</sup> = Z<sup>n</sup>

#### kbd
    Press <kbd><kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>Delete</kbd></kbd> to end the session.
Press <kbd><kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>Delete</kbd></kbd> to end the session.

#### mark
    Most <mark>salamanders</mark> are nocturnal, and hunt for insects, worms, and other small creatures.
Most <mark>salamanders</mark> are nocturnal, and hunt for insects, worms, and other small creatures.

***

### 超链接图片

[![小刘](https://mimao-blog.netlify.app/avatar.png)]("超链接" https://mimao-blog.netlify.app/avatar.png)

***

### 嵌入Html5代码块

<svg class="canon" xmlns="http://www.w3.org/2000/svg" overflow="visible" viewBox="0 0 496 373" height="373" width="496"><g fill="none"><path stroke="#000" stroke-width=".75" d="M.599 372.348L495.263 1.206M.312.633l494.95 370.853M.312 372.633L247.643.92M248.502.92l246.76 370.566M330.828 123.869V1.134M330.396 1.134L165.104 124.515"></path><path stroke="#ED1C24" stroke-width=".75" d="M275.73 41.616h166.224v249.05H275.73zM54.478 41.616h166.225v249.052H54.478z"></path><path stroke="#000" stroke-width=".75" d="M.479.375h495v372h-495zM247.979.875v372"></path><ellipse cx="498.729" cy="177.625" rx=".75" ry="1.25"></ellipse><ellipse cx="247.229" cy="377.375" rx=".75" ry="1.25"></ellipse></g></svg>

{{< css.inline >}}
<style>
.canon { background: white; width: 100%; height: auto; }
</style>
{{< /css.inline >}}

```
<svg class="canon" xmlns="http://www.w3.org/2000/svg" overflow="visible" viewBox="0 0 496 373" height="373" width="496"><g fill="none"><path stroke="#000" stroke-width=".75" d="M.599 372.348L495.263 1.206M.312.633l494.95 370.853M.312 372.633L247.643.92M248.502.92l246.76 370.566M330.828 123.869V1.134M330.396 1.134L165.104 124.515"></path><path stroke="#ED1C24" stroke-width=".75" d="M275.73 41.616h166.224v249.05H275.73zM54.478 41.616h166.225v249.052H54.478z"></path><path stroke="#000" stroke-width=".75" d="M.479.375h495v372h-495zM247.979.875v372"></path><ellipse cx="498.729" cy="177.625" rx=".75" ry="1.25"></ellipse><ellipse cx="247.229" cy="377.375" rx=".75" ry="1.25"></ellipse></g></svg>

\{\{< css.inline >\}\}
<style>
.canon { background: white; width: 100%; height: auto; }
</style>
\{\{< /css.inline >\}\}
```

***

### emoji 表情符号

表情符号可以通过多种方式在Hugo项目中启用。
(设置 enableEmoji: true 即可)
[Emoji cheat sheet](http://www.emoji-cheat-sheet.com/) 是表情符号速记代码的有用参考。

<p><span class="nowrap"><span class="emojify">🙈</span> <code>:see_no_evil:</code></span>  <span class="nowrap"><span class="emojify">🙉</span> <code>:hear_no_evil:</code></span>  <span class="nowrap"><span class="emojify">🙊</span> <code>:speak_no_evil:</code></span></p>
<br>
{{< css.inline >}}
<style>
.emojify {
	font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
	font-size: 2rem;
	vertical-align: middle;
}
@media screen and (max-width:650px) {
  .nowrap {
    display: block;
    margin: 25px 0;
  }
}
</style>
{{< /css.inline >}}

```
<p>
  <span class="nowrap">
    <span class="emojify">🙈</span> 
    <code>:see_no_evil:</code>
  </span>  
  <span class="nowrap">
    <span class="emojify">🙉</span>
    <code>:hear_no_evil:</code>
  </span>  
  <span class="nowrap">
    <span class="emojify">🙊</span> 
    <code>:speak_no_evil:</code>
  </span>
</p>
<br>
\{\{< css.inline >\}\}
<style>
.emojify {
  font-family: Apple Color Emoji, Segoe UI Emoji, NotoColorEmoji, Segoe UI Symbol, Android Emoji, EmojiSymbols;
  font-size: 2rem;
  vertical-align: middle;
}
@media screen and (max-width:650px) {
  .nowrap {
    display: block;
    margin: 25px 0;
  }
}
</style>
\{\{< /css.inline >\}\}
```
***

### 数学表达式

#### 表达式

{{< math.inline >}}
<p>
Inline math: \(\varphi = \dfrac{1+\sqrt5}{2}= 1.6180339887…\)
</p>
{{</ math.inline >}}

Block math:
$$
 \varphi = 1+\frac{1} {1+\frac{1} {1+\frac{1} {1+\cdots} } } 
$$

```
\{\{< math.inline >\}\}
<p>
Inline math: \(\varphi = \dfrac{1+\sqrt5}{2}= 1.6180339887…\)
</p>
\{\{</ math.inline >\}\}

Block math:
$$
 \varphi = 1+\frac{1} {1+\frac{1} {1+\frac{1} {1+\cdots} } } 
$$
```

了解更多数学表达式的写法 请参阅[Supported TeX Functions](https://katex.org/docs/supported.html)

***

### bilibili 短代码

    \{\{< bilibili av498363026 >\}\}
{{< bilibili av498363026 >}}

***

### Gist 短代码

    \{\{< gist spf13 7896402 >\}\}
{{< gist spf13 7896402 >}}

***

### Gitlab代码片段 短代码

    \{\{< gitlab 2349278 >\}\}
{{< gitlab 2349278 >}}

***

### Quote 短代码

{{< quote author="A famous person" source="The book they wrote" url="https://en.wikipedia.org/wiki/Book">}}
quote author source url
{{< /quote >}}

{{< quote source="Anonymous book" url="https://en.wikipedia.org/wiki/Book">}}
quote source url
{{< /quote >}}

{{< quote source="Some book">}}
quote source
{{< /quote >}}

{{< quote author="Somebody">}}
quote author
{{< /quote >}}

```
\{\{< quote author="A famous person" source="The book they wrote" url="https://en.wikipedia.org/wiki/Book">\}\}
quote author source url
\{\{< /quote >\}\}

\{\{< quote source="Anonymous book" url="https://en.wikipedia.org/wiki/Book">\}\}
quote source url
\{\{< /quote >\}\}

\{\{< quote source="Some book">\}\}
quote source
\{\{< /quote >\}\}

\{\{< quote author="Somebody">\}\}
quote author
\{\{< /quote >\}\}
```