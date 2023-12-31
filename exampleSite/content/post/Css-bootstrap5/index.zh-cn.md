---
# 帖子的发布作者
author: mimao
# 帖子的标题
title: 初识 bootstrap5
# 帖子的日期
date: 2023-07-07
# 帖子的描述
description: 初识bootstrap5并快速对bootstrap5框架进行了解
# 帖子的标签
tags:
  - bootstrap5
# 帖子分类
categories:
  - Css
---

# BootStrap5

## 简介

### 常识
```
在html中，
包括 <meta name=“viewport”>标记，以便在移动设备中进行正确的响应行为
包含 popper模块，才可以用下拉菜单、弹出窗口和工具提示(即：dropdowns, poppers,tooltips)消除通知;

用于切换状态和复选框/单选功能的按钮;

所有幻灯片行为、控件和指示器的旋转木马;

用于切换内容可见性的折叠;

用于显示和定位的下拉菜单（也需要Popper）;

用于显示、定位和滚动行为的模式;

用于扩展Collapse和Offcanvas插件以实现响应行为的导航栏;

使用Tab插件切换内容窗格的导航;

用于显示、定位和滚动行为的非画布;

Scrollspy用于滚动行为和导航更新;

用于显示和消除的Toast

用于显示和定位的工具提示和弹出窗口（也需要Popper）
```

```
在html中，文档结构中需要有
(1).HTML5文档类型 
<!doctype html>
<html lang="en">
  ...
</html>

(2).响应元标签
<meta name="viewport" content="width=device-width, initial-scale=1">
```	
		
### 框架的使用

```
html javascript中使用cdn或使用 源文件
css
	单独引入(只引入的部分)
		Content部分
			bootstrap-reboot.css或bootstrap-reboot.min.css
		Utilities部分
			bootstrap-utilities.css或bootstrap-utilities.min.css
	全部引入
		bootstrap.css或bootstrap.min.css
js
	全部引入(包含popper)
		bootstrap.bundle.js或bootstrap.bundle.min.js
	除popper之外其他部分都引入
		bootstrap.js或bootstrap.min.js
	
```

```
css样式

响应式符号介绍

各个符号对应的设备名称和最小屏幕宽度范围，（该符号屏幕是 大于等于最小屏幕宽度范围）单位：px

sm  平板  576

md  桌面显示器  768

lg  大桌面显示器 992

xl  特大桌面显示器  1200

xxl 超大桌面显示器  1400
```

```
容器
.container
.container-sm
.container-md
.container-lg
.container-xl
.container-xxl

对于sm md lg xl xxl  不同尺寸型号的设备

如果设置为md则对应小于md型号的 container应用的div，宽度会设置为100%  而对于等于大于该设备尺寸的，则会有一个固定宽度

其他型号的，同理可得
.container-fluid
宽度会一直 保持100%
共同之处，当.container宽度处于100%时，对应的功能与.container-fluid 一致，对应的边距时一样的
```

```
行 和 列

基本用法
简介
列必须放置在行中才有效果
并且 一行可以设置等于小于12列
大于的部分，会换行

用法
.col-
.col-sm-
.col-md-
.col-lg-
.col-xl-
.col-xxl-

- 符号的后面可以取  1   ~  12 的数字

例如：
<div class="row">
	<div class="col-md-4">4</div>
	<div class="col-md-4">4</div>
	<div class="col-md-4">4</div>
</div>
注意：这个只是对于水平方向的效果，高度还需自己设置
```

```
列偏移
offset-sm-
offset-md-
offset-lg-
offset-xl-
offset-xxl-
```	

```
列排序
				order-
				注意排序规则：

没有设置 order-  的列会排在设置了order-列的前面
		标题排版
			h1~h6
				.h1  .h2 .h3 .h4 .h5 .h6  加上这些类就会有对应标题符号的效果
				.display-1 .display-2 ~ .display-6   会让字体变得更大
				.lead  会突出显示段落
				small标签，会让字体变小并且颜色也会变浅
				.small 类，则会让字体变为父容器字体大小的 85%    让字体变小
		文本操作
			文本对齐
				text-
					普通对齐
						text-start
text-center
text-end
					响应式对齐（根据屏幕大小进行对齐）
						text-(sm/md/lg/xl/xxl)-(start/center/end)
					注意，如果需要设置sm一下的对其和sm以上的对其不一样，则可以：

class="text-start text-sm-end text-md-start ...."    即可
			文本大小写设置
				text-lowercase  文本小写

text-uppercase  文本大写
			单词首字母设置
				text-capitalize   将单词首字母大写
			截断文本用省略号表示超出部分
				text-truncate
			文本换行和溢出(不换行 文本溢出元素)
				换行
					text-wrap
				溢出
					text-nowrap
			文本实现划线效果和去除a链接的下划线效果
				text-decoration-none
					去除下划线
				text-decoration-underline
					文本添加下划线的效果
				text-decoration-line-through
					在文本中间添加一行
		字体操作
			字体大小
				.fs-1
.fs-2
.fs-3
.fs-4
.fs-5
.fs-6

字体大小从1至6 依次变小（最后fs-6的大小 与 默认大小相等）
					对应css是：font-size:
			字体倾斜加粗
				加粗
					.fw-bolder
.fw-bold
.fw-normal
.fw-light
.fw-lighter


normal对应加粗400（即正常的字体粗细）
bold对应  700
light对应 300
						对应css是：font-weight
				斜体
					.fst-italic 倾斜

.fst-normal 取消倾斜
						对应css是：font-style:italic;
		行高
			简介
				在bootstrap中默认的行高为 1.5
			.lh-
				1
					代表 1rem
				sm
					代表 1.25rem
				base
					代表 1.5rem
				lg
					代表 2rem
			即：

.lh-1
.lh-sm
.lh-base
.lh-lg
		字体颜色
			黑色
				text-body
			白色
				text-white
			灰色
				深灰
					text-dark
				灰色
					text-secondary
						用于副标题
				浅灰
					text-muted
				接近白色的浅灰色
					text-light
			蓝色
				蓝色
					text-primary
						定义比较重要的文本时用到
				浅蓝色
					text-info
						定义 信息之类的文本用到
			绿色
				浅绿色
					text-success
						定义 成功之类的文本用到
			黄色
				黄色
					text-warning
						定义警告之类的文本用到
			红色
				红褐色
					text-danger
						定义一些危险之类的文本用到
			注意：（可设置透明度）
				在text-(color)-数字     该数字可以设置为0~100     代表 0%~100%的透明度
				例如：

text-black-50

text-white-50
		背景颜色
			同理可得
				同字体颜色一样的参数，但只需将 text替换为 bg即可
		列表
			去掉列表的原有样式
				.list-nostyled
			内联列表
				在 ul标签中，class="list-inline"  li中，class="list-inline-item"
			列表组
				ul中，class="list-group"  li中，class="list-group-item"
				li标签中
					.active
						被选择样式
					.disabled
						已禁用样式
					只有这个样式效果，但如果li 中内置了a标签，其标签还可以使用，只是li标签会看起来有点灰色
			链接列表组
				在ul中，class="list-group"，将li标签换为 a标签 并在a标签中页添加class="list-group-item"
				a标签中，
					如果需要悬停效果，还可以在a标签中，添加 class="list-group-item-action"
			列表详情标签
				dl < dt dd
				可以结合 row col 进行布局
			移除列表边框
				在ul中，除了添加 .list-group  还要添加 .list-group-flush，这样就将列表中的边框去除了
			水平列表组
				在ul中，除了添加.list-group  还要添加 .list-group-horizontal
			数字编号列表组
				在ul中，除了添加.list-group  还要添加 .list-group-numbered
			带徽章的列表项
				在 列表项中，添加一个 带有 .badge 的元素即可
			自定义列表项
				定义列表项 头部样式   列表项中添加： .list-group-item-heading
				定义列表项 内容样式   列表项中添加： .list-group-item-text
		徽章
			.badge
			还可以添加 .rounded-pill    来达到 药丸型的徽章
			注意，默认情况  徽章中的字体是白色，需要添加背景色
			使用 bg-颜色    即可
		表格
			基础表格
				基本表格结构
					<table>
	<thead>
		<tr>
			<td></td>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td></td>
		</tr>
	</body>
</table>
				基本样式
					添加 .table 就可以实现基本的表格样式
					添加 .table-颜色  添加到table中， 即可实现table颜色的定义，即背景颜色的定义
						也可以添加到 tr中 来实现tr的背景颜色的效果
					添加 .table-striped  即可实现表格带条纹的效果
					添加 .table-bordered  即可实现 带边框的表格效果
					添加 .table-borderless  即可实现 没有任何边框的表格效果
					添加 .table-hover  即可实现  鼠标在每行上的悬停效果
					添加  .table-sm  来减少内边距，即可实现  表格更加紧凑
					在 table外添加一个div，然后，该div中，添加.table-responsive  即可实现 响应式表格（即 自动显示滚动条）

还可以设置根据视图大小，来确定是否显示滚动条 即： .table-responsive-(sm/md/lg/xl/xxl)
		图片
			.rounded  添加圆角
			.rounded-circle   添加椭圆形效果
			.img-thumbnail   添加缩略图效果
			.float-start  图片左对齐    .float-end  图片右对齐
			.mx-auto .d-block  来实现图片剧中对其（即：css样式中，display:block;margin:auto;）
			.img-fluid    来实现响应式图片的效果（即：css样式中，width:100%;height:auto;）
		按钮
			基础按钮
				.btn   会有一个圆角的样式效果，但没有边框，是一个基本的按钮
			其他按钮样式
				颜色
					.btn-颜色   为按钮实现背景色的效果   .btn-primary
						.btn-link 可以实现链接按钮的效果
				颜色 外观
					.btn-outline-颜色
						会生成有边框，鼠标悬浮上去，有突出显示的效果
				尺寸
					.btn-lg
						大按钮
					.btn-sm
						小按钮
					.btn-block  在父元素中， .d-gird
						块级按钮（会横跨整个父元素的宽度，父元素是多宽，则该按钮就会是多宽）
				按钮状态
					激活状态
						.active
					禁用状态
						.disabled
					注意，只是设置样式效果，如果是对 a链接进行设置，虽然添加了.diabled，但还是可以进行点击的  除非删除href属性
				按钮组
					基本的按钮组
						在按钮的父元素上， 添加 .btn-group 即可
					按钮组大小
						在 按钮的父元素上， 同一设置大小即可设置所有在父元素中的按钮大小，让其保持一致
						.btn-group  .btn-group-(lg/xs/sm)   即： lg大按钮  xs默认大小的按钮  sm小按钮
					垂直按钮组
						只需要 将 .btn-group替换为  .btn-group-vertical    大小设置是一样的
		加载器
			基础加载器
				.spinner-border    就可以实现加载器的效果
			闪烁加载器
				.spinner-grow   就可以实现闪烁加载器的效果
			其他样式
				颜色
					直接使用文本颜色类即可
						即：text-颜色
				尺寸
					基础：
						小尺寸   .spinner-border-sm
					闪烁：
						小尺寸   .spinner-grow-sm
			带有颜色的列表项
				只需在列表项中，添加  .list-group-item-颜色     即可
		进度条
			基础进度条
				在父元素中，添加 .progress   子元素中，添加 .progress-bar 
			条纹进度条
				在父元素中，添加 .progress   子元素中，添加 .progress-bar .progress-bar-striped
			条纹动画进度条
				在父元素中，添加 .progress   子元素中，添加 .progress-bar .progress-bar-striped .progress-bar-animated
			混色进度条
				在父元素中，添加 .progress   设置多个子元素，并添加 .progress-bar 对于每个子元素，可以设置不同背景颜色，即可实现混色进度条
			设置颜色，在子元素中进行设置即可，添加  bg-颜色  即可设置
			设置进度，只需为子属性 添加 width内联属性
			设置进度文字，只需在子元素中，设置其文本，即 在div中，只需在标签对中间写下进度文字即可
			进度条 示例代码
				例如：
基本进度条：

<div class="progress">
	<div class="progress-bar bg-primary" style="width:20%;">20%</div>
</div>

条纹进度条：
<div class="progress">
	<div class="progress-bar bg-primary progress-bar-striped" style="width:20%;">20%</div>
</div>

条纹动画进度条：
<div class="progress">
	<div class="progress-bar bg-primary progress-bar-striped progress-bar-animated" style="width:20%;">20%</div>
</div>

混色进度条：（需要注意 混色进度条，所有子元素的width的百分比之和不能大于 100%）
<div class="progress">
	<div class="progress-bar bg-primary" style="width:20%;">20%</div>
	<div class="progress-bar bg-warning" style="width:20%;">20%</div>
	<div class="progress-bar bg-info" style="width:20%;">20%</div>
</div>
		边框
			基础边框
				.border
			其他样式
				颜色
					.border-颜色
				宽度
					.border-宽度
						宽度可以是 任意数字   单位: px
					设置 方向上的宽度
						.border-方向-宽度
						方向：  top bottom start end
				方向上的设置边框
					.border-方向
		圆角边框
			基础圆角边框
				.rounded
			椭圆形圆角边框
				.rounded-circle
			胶囊型圆角边框
				.rounded-pill
			其他样式
				方向上的设置边框圆角
					.rounded-方向

从左上角 顺时针：
top  左上角和右上角
end	右上角和右下角
bottom 左下角和右下角
start 左上角和左下角
				从元素中删除圆角样式
					.rounded-0
				圆角半径
					.rounded-1	设置半径为 0.2rem

.rounded-2 设置半径为 0.25rem

.rounded-3 设置半径为 0.3rem
		浮动和清除浮动
			左浮动   .float-start
			右浮动  .float-end
			清除浮动  .clearfix
			响应式浮动
				根据屏幕尺寸进行选择是否浮动
				.float-（sm/md/lg/xl/xxl）-(start/end)
		块级元素居中
			.mx-auto
		高度
			设置高度为父容器高度的百分比
				例如： 
.h-100   设置高度为父容器高度的 100%
.h-20	 设置高度为父容器高度的 20%
			高度自动
				.h-auto
			最大 最小视图高度  视图高度
				最大高度
					.mh-100   设置最大高度为父容器高度的 100%
				最小视图高度
					.min-vh-100   最小视图高度为 100vh
				视图高度
					.vh-100  高度为 100vh
		宽度
			设置宽度为父容器宽度的百分比
				例如： 
.w-100   设置宽度为父容器宽度的 100%
.w-20	 设置宽度为父容器宽度的 20%
			宽度自动
				.w-auto
			最大 最小视图宽度  视图宽度
				最大宽度
					.mw-100   设置最大宽度为父容器宽度的 100%
				最小视图宽度
					.min-vw   最小视图宽度为 100vw
				视图宽度
					.vw-100  宽度为 100vw
		vh vw单位：
			100vh 相当于浏览器的高度   即：视口的高度
			100vw 相当于浏览器的宽度   即：视口的宽度
		外间距 和 内间距
			外间距 用 m表示
			内间距 用 p表示
			两者用法一致
			用法
				.(m/p)方向-大小数值
				方向
					t 上
						即：垂直方向上的 top
					b 下
						即：垂直方向上的 bottom
					s 左
						即：水平方向上的 start
					e  右
						即：水平方向上的 end
					x 左右
						即：水平方向
					y 上下
						即：垂直方向
				大小
					0
						取消该方向上的边距
					1
						0.25rem
					2
						0.5rem
					3
						1rem
					4
						1.5rem
					5
						3rem
					margin,padding 只能取值：  0~5  但margin还可以取auto，在 mx:auto；时效果为，块级元素可实现居中对齐
				例如：

.mt-0   相当于css中：margin-top:0px;

.mtb-1	   相当于css中：margin-top:0.25rem; margin-bottom:0.25rem;

.mx-5	   相当于css中：margin-left:3rem; margin-right:3rem;
			响应式外间距
				.m(方向)-(sm/md/lg/xl/xxl)-大小
		阴影
			.shadow
			.shadow-lg   大阴影
			.shadow-sm 小阴影
			.shadow-none  去除阴影
		flex容器
			普通的flex容器
				.d-flex
			行内flex容器
				.d-inline-flex
					与普通flex容器区别是，如果都没有定义宽度，行内容器宽度只会占内容的宽度
			其他样式
				容器的样式
					容器内元素的布局方向
						水平方向
							.flex-row   默认（水平方向）
						垂直方向
							.flex-cloumn
								垂直方向
						反转start end的方向
							.flex-row-reverse   水平方向上， 将起始位置设置为 右边（即：向右对齐）
							.flex-cloumn-reverse   垂直方向上， 将起始位置设置为 底部（即：向底部对齐）
					换行
						.flex-wrap  换行
						.flex-nowrap  不换行  （默认）
						.flex-wrap-reverse  换行，且第一行放置到最下面
					容器内元素的布局方式
						水平方向
							默认值：  如果没有设置，默认为 start对齐
							justify-content-(start/end/center/between/round)

start  起始方向对齐 end结束位置对齐 center居中对齐 between两端对齐 round 元素两侧间隔相等的对齐
						垂直方向
							默认值：如果没有设置，默认为 stretch   容器内元素高度自适应
							align-item-(start/end/center/baseline/stretch)

start  起始方向对齐 end结束位置对齐 center居中对齐
baseline 是根据一行中第一个文字的基线进行对齐，即文字底部的基线
stretch  元素高度自适应
				容器内元素的样式
					排序
						.order-(数字)   与网格中 列的.order-(数字) 的使用规则是一样的   
 
没有设置order-（数字） 的默认为0，order-数字中的数字越大，越会排在后面
					等宽
						.flex-fill    强制使设置了该类进行等宽，其余没有设置的保持不变，设置了该类的，强制等分占满多余空间
					伸展
						.flex-grow-0
							该元素不进行扩展
						.flex-grow-1
							则该元素在父容器还有多余空间时 占满多余的空间
					自定义自己在容器内，垂直方向上的对齐方式
						该元素自定义自己的对齐方式，其他的不受影响
						.align-self-(start/end/center/baseline/stretch)
			响应式flex布局
				容器
					.d-(sm/md/lg/xl/xxl)-flex
					.d-(sm/md/lg/xl/xxl)-inline-flex
				方向
					水平方向
						.flex-(sm/md/lg/xl/xxl)-row
						.flex-(sm/md/lg/xl/xxl)-row-reverse
					垂直方向
						.flex-(sm/md/lg/xl/xxl)-cloumn
						.flex-(sm/md/lg/xl/xxl)-cloumn-reverse
				.....
					一般在 flex前面添加  d后面添加  完整属性名称后，属性值前进行添加响应式符号
		css中flex容器内元素的属性介绍
			order属性
				order:数字    数字必须时整数，可正可负，可为0      

数字越小视图上显示就越靠前，它只改变视图效果，不改变html结构

没有设置的元素，默认为：0
			flex-grow
				默认值： 0
				不能设置为负数
					任意整数小数都行
				设置为：0  则代表不参与容器剩余空间分配
				如果所有设置了该属性的元素属性值和小于1，则代表不完全 分配空间
				大于等于1的，则代表可以完全分配空间
				但 不管是 小数还是大于1的整数，

1.如果容器中有空间，而且还有其他元素也设置了该属性大于0，
则一起分配剩余空间，（按比例进行分配）

2.如果容器中有空间，但所有设置了该属性的元素值之和小于1，
则 每一个可分配的宽度大小等于： 剩余空间*该元素的flex-grow值 除以 1可得（即：剩余空间*该元素的flex-grow值）
			flex-shrink
				默认值：1
				不能设置为负数
					任意整数小数都行
				设置为：0  则代表不参与超出容器部分的元素缩小
				如果所有设置了该属性的元素属性值和小于1，则代表不完全缩小元素，达到超出部分缩小到不超出容器
				大于等于1的，则代表可以缩小项目 达到元素不超出容器的目的
				但 不管是 小数还是大于1的整数，如果元素超出容器，而且还有其他元素也设置了该属性大于0，

则一起缩小 腾出空间，让元素不在超出容器，（按比例进行缩小）

计算方法：
比例（不管所有元素设置的flex-shrink的值是否小于1都要用到）：



(1)溢出部分宽度 等于 所有元素的宽度之和 减去 容器宽度 可得

(2)总参与缩小的元素每一个元素宽度*所设置的flex-shrink值，之和 即：总比例数

(3)每一个的比例计算等于： 参与缩小元素的宽度*flex-shirink值 除以 总比例数 可得

1.如果所有参与元素flex-shrink值之和大于1：
每一个元素缩小的宽度是：  溢出部分宽度*每个元素的缩小比例 可得

2.如果小于1:
所有元素需要缩小的量等于： 300*(每一个元素的flex-shrink值之和)  可得

每一个元素缩小的宽度是： 所有元素需要缩小的量*每一个元素溢出的比例
			flex-basis
				为容器中，设置元素主轴方向的固定宽度
				默认： auto   可以设置大小 单位px
				注意，它与 width不同
					但容器中元素内容主轴方向大于设定的大小，则元素会变大，而不会让元素内容溢出，而width会固定大小，里面内容则会溢出
			flex
				flex是 flex-grow flex-shrink flex-basis 三个属性的缩写  默认值： 0 1 auto
				flex可以简写为：  flex:1;  则代表： flex-grow:1;flex-shrink:1;flex-basis:0%; 

0%指没有宽度 auto指 如果设置了width，则该元素的基准值为 width值
			algin-self
				针对该元素进行自定义对齐方式，其他元素不受影响
				取值：
					auto   默认（与容器的对齐方式一致）
					flex-start
						顶端对齐
					flex-end
						底部对齐
					center
						居中对齐
					baselinne
						第一行文字的底线对齐（即 改文字的基线对齐）
					stretch
						当元素未设置高度时，该元素的高度会与容器等高对齐
	js组件
```
