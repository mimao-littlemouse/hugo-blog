---
# 帖子的发布作者
author: mimao
# 帖子的标题
title: 初识 Markdown
# 帖子的日期
date: 2023-07-07
# 帖子的描述
description: 初识Markdown并快速对其进行了解
# 帖子的标签
tags:
  - markdown
# 帖子分类
categories:
  - Markdown
---

# markdown介绍
**Markdown 是一种轻量级的标记语言，可用于在纯文本文档中添加格式化元素。**
**Markdown 由 John Gruber 于 2004 年创建，如今已成为世界上最受欢迎的标记语言之一。**
Markdown是一种轻量级标记语言，排版语法简洁，让人们更多地关注内容本身而非排版。它使用易读易写的纯文本格式编写文档，可与HTML混编，可导出 HTML、PDF 以及本身的 .md 格式的文件。因简洁、高效、易读、易写，Markdown被大量使用，如Github、Wikipedia、简书等。
***使用原因***
* Markdown 无处不在。StackOverflow、CSDN、掘金、简书、GitBook、有道云笔记、V2EX、光谷社区等。主流的代码托管平台，如 GitHub、GitLab、BitBucket、Coding、Gitee 等等，都支持 Markdown 语法，很多开源项目的 README、开发文档、帮助文档、Wiki 等都用 Markdown 写作。

Markdown 是纯文本可移植的。几乎可以使用任何应用程序打开包含 Markdown 格式的文本文件。如果你不喜欢当前使用的 Markdown 应用程序了，则可以将 Markdown 文件导入另一个 Markdown 应用程序中。这与 Microsoft Word 等文字处理应用程序形成了鲜明的对比，Microsoft Word 将你的内容锁定在专有文件格式中。

Markdown 是独立于平台的。你可以在运行任何操作系统的任何设备上创建 Markdown 格式的文本。

Markdown 能适应未来的变化。即使你正在使用的应用程序将来会在某个时候不能使用了，你仍然可以使用文本编辑器读取 Markdown 格式的文本。当涉及需要无限期保存的书籍、大学论文和其他里程碑式的文件时，这是一个重要的考虑因素

## Markdown 标记语言
#### 目录
一.[标题](#title_1)
二.[段落和换行](#title_2)
三.[文字粗体 斜体 粗体加斜体](#title_3)
四.[列表和引用以及转义标识和转义字符语法](#title_4)
五.[分割线和代码块](#title_5)
六.[链接和图片](#title_6)
七.[Markdown扩展语法](#title_7)

***
## 语法介绍
##### (书写符号与内容之间，最好用空格隔开)
### 一.标题 {#title_1}
#### (1)标题共有6级
1. ##### 一级标题 `#`   
2. ##### 二级标题 `##`
3. ##### 三级标题 `###`
4. ##### 四级标题 `####`
5. ##### 五级标题 `#####`
6. ##### 六级标题 `######`
#### (2)效果
# 一级标题 `#`   
## 二级标题 `##`
### 三级标题 `###`
#### 四级标题 `####`
##### 五级标题 `#####`
###### 六级标题 `######`
#### （3）其他扩展
1. ##### 一级标题
###### 在文字的下方添加 `= `
###### `=` 的数量可以是任意的，但最少一个
2. ##### 二级标题
###### 在文字的下方添加 `-`
###### `-` 的数量可以是任意的，但最少一个
***
### 二.段落和换行 {#title_2}
1. #### 段落
   - 要创建段落，请使用空白行 对文本进行分隔
   - 不要用`空格`或`tab键`缩进段落
2. #### 换行
   - 使用回车键进行换行即可 (推荐)
   - > 其他换行方式，比如添加 `<br>` 或 `行尾添加空格` 或 `\反斜杠` (不推荐)
***
### 三.文字粗体 斜体 粗体加斜体 {#title_3}
1. #### 斜体
   - 使用 `*文字*` 表示即可
   - 例如：*文字*
2. #### 粗体
   - 使用 `**文字**` 表示即可
   - 例如：**文字**
3. #### 粗体加斜体
   - 使用 `***文字**` 表示即可
   - 例如：**文字**
4. #### 其他方式并不推荐
***
### 四.列表和引用以及转义标识和转义字符语法 {#title_4}
1. #### 列表
   - 有序列表
     - 使用 `1. ` （序号.空格隔开写内容 ） 
   - 无序列表
     - 使用 `- ` （-空格隔开写内容）
2. #### 引用
    - 使用 `>` 进行表示该段为引用，该符号可以进行嵌套使用，嵌套越多，缩进越明显
    - 例如：`> 内容` `>> 内容`
    - 效果：
    - 1. > 一个引用
    - 2. >> 两个英勇
    - 3. >>>>> 甚至多个
    - 4. 嵌套使用：
> hello
>> hello
>>> world
    - 搭配列表和``代码标识进行使用，效果明显
3. #### 转义标识
   - 使用 `` 进行标识
   - 效果： `效果`
4. #### 转义字符语法
   - 使用 `\` 进行转义即可
   - 例如：`*` 需要显示出来 就可以使用 `\*` 进行转义显示
***
### 五.分割线和代码块 {#title_5}
1. #### 分割线
   - 使用 `***` 在新的一行开头书写，并且当前这行无其他内容即可
   - 效果如下
***
2. #### 代码块
   - > 在用`#`标识的标题下方，只需要一个`tab键` 
   - > 在其他地方，则需要先用空行隔开其他内容 开头处需要三个 `tab键`
   - 效果如下

            效果
***
### 六.链接和图片 {#title_6}
1. #### 链接
   1. 链接语法：`[链接显示的名称](链接的地址 "链接的title属性")`
      - 例如：`[百度](http://www.baidu.com "百度地址")`
      - 效果如下
      - [百度](http://www.baidu.com "百度地址")
      - 在[百度]中变为[`百度`]，加上转义标识，之后，效果如下：
      - [`百度`](http://www.baidu.com "百度地址")
2. #### 图片
   1. 图片语法: `![图片的alt属性](图片的链接地址 "图片的title属性")`
      - 例如：`![百度图片](./baidu.png "百度")` 
      - 效果如下
      - ![百度图片](./baidu.png "百度")
***
### 七.Markdown扩展语法 {#title_7}
1. #### 表格
例如
: `|列名1|列名2|列名3|`
`|:-|:-:|-:|`
`|默认对其方式(左对齐)|中间对齐|右对齐|`
`|内容1|内容2|内容3|`

***效果***
|列名1(------)|列名2(------)|列名3(------)|
|:-|:-:|-:|
|默认对其方式(左对齐)|中间对齐|右对齐|
|内容1|内容2|内容3|
***
2. #### 代码块
###### 不写语言类型，则表示原样输出
例如
: 使用 ` ```语言类型 换行另起一行书写内容 ``` `

\`\`\`
let a = 1;
\`\`\`
效果如下
```
let a = 1;
```
***
\`\`\`javascript
let a = 1;
\`\`\`

效果如下
```javascript
let a = 1;
```
***
3. #### 脚注
   - 1. 使用 [^脚注名] 定义 
   - 2. 使用[^脚注名]: 进行激活
   - - 激活之后，才会有效果
   - 效果如下
脚注[^7-3] 
[^7-3]: 这就是7-3的脚注
   
4. #### 标题编号
   - 1. 使用 {#名称} 进行定义
   - 2. 使用 `[链接名称](#名称)` 进行链接使用
效果如下
[链接名称](#名称)
***
5. #### 定义学术列表
语法如下
```
学术名称
: 学术内容
学术内容
```
效果如下

学术名称
: 学术内容
学术内容

6. #### 删除线
语法如下
```
~~内容~~
```
效果如下
~~内容~~

7. #### 任务列表
语法如下
```
- [ ] 列表1
- [x] 列表2
```
效果如下
- [ ] 列表1
- [x] 列表2
  
8. #### Emoji表情
在网站上，复制下来，进行粘贴即可

链接地址
: [emoji](https://emojipedia.org/ "Emoji表情")


   
