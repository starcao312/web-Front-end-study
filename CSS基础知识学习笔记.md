## CSS 基础知识学习笔记

### 1. 语法

```css
/*CSS声明总是以分号(;)结束，声明总以大括号({})括起来:*/
p {
	color: red;
	text-align: center;
}
```

### 2. id 和 class 选择器

```css
/*
* HTML元素以id属性来设置id选择器,CSS 中 id 选择器以 "#" 来定义。
* class 选择器用于描述一组元素的样式，class 选择器有别于id选择器，class可以在多个元素中使用。
* class 选择器在HTML中以class属性表示, 在 CSS 中，类选择器以一个点"."号显示。
*/
#pare1 {
	color: orange;
	text-align: center;
}
.pare2 {
	font-family: "Time New Roman";
	font-size: 20px;
}
/*
*也可以指定特定的HTML元素使用class,在以下实例中, 所有的 p 元素使用 class="center" 让该元素的文本居中:
*/
p.center {
	text-align: center;
}
```

### 3. CSS 创建

```css
/*
* <link rel="stylesheet" type="text/css" href="mystyle.css">
* 假如拥有内部样式表的这个页面同时与外部样式表链接，内部样式表中的样式会将外部样式表会取代
*/
/* 外部样式 */
h3{
    color:red;
    text-align:left;
    font-size:100pt;
}
/* 内部样式 */
h3{
    text-align:right;
}
/* 内联样式 */
<p style="color:sienna;margin-left:20px">这是一个段落。</p>
```

-   优先级：(内联样式）Inline style > （内部样式）Internal style sheet >（外部样式）External style sheet > 浏览器默认样式

### 4. CSS 背景

-   background-color：定义了元素的背景颜色.
-   background-image：描述了元素的背景图像.（默认情况下 background-image 属性会在页面的水平或者垂直方向平铺。）
-   background-repeat：设置背景图像是否及如何重复。
-   background-attachment：背景图像是否固定或者随着页面的其余部分滚动。
-   background-position：改变图像在背景中的位置

### 5. CSS 文本属性

| 属性            | 描述                                         |
| :-------------- | :------------------------------------------- |
| color           | 设置文本颜色                                 |
| direction       | 设置文本方向。                               |
| letter-spacing  | 设置字符间距                                 |
| line-height     | 设置行高                                     |
| text-align      | 对齐元素中的文本                             |
| text-decoration | 向文本添加修饰（主要是用来删除链接的下划线） |
| text-indent     | 缩进元素中文本的首行                         |
| text-shadow     | 设置文本阴影                                 |
| text-transform  | 控制元素中的字母                             |
| unicode-bidi    | 设置或返回文本是否被重写                     |
| vertical-align  | 设置元素的垂直对齐                           |
| white-space     | 设置元素中空白的处理方式                     |
| word-spacing    | 设置字间距                                   |

### 6. CSS 链接

```css
/* 字体颜色 */
a:link {
	color: #000000;
} /* 未访问链接*/
a:visited {
	color: #00ff00;
} /* 已访问链接 */
a:hover {
	color: #ff00ff;
} /* 鼠标移动到链接上 */
a:active {
	color: #0000ff;
} /* 鼠标点击时 */
/* 下划线 */
a:link {
	text-decoration: none;
} /* unvisited link */
a:visited {
	text-decoration: none;
} /* visited link */
a:hover {
	text-decoration: underline;
} /* mouse over link */
a:active {
	text-decoration: underline;
} /* selected link */
/* 背景颜色 */
a:link {
	background-color: #b2ff99;
} /* 未访问链接 */
a:visited {
	background-color: #ffff85;
} /* 已访问链接 */
a:hover {
	background-color: #ff704d;
} /* 鼠标移动到链接上 */
a:active {
	background-color: #ff704d;
} /* 鼠标点击时 */
/* 创建链接框 */
a:link,
a:visited {
	display: block;
	font-weight: bold;
	color: #ffffff;
	background-color: #98bf21;
	width: 120px;
	text-align: center;
	padding: 4px;
	text-decoration: none;
}
a:hover,
a:active {
	background-color: #7a991a;
}
```

### 7. 盒子模型演示

1. CSS css 盒子模型 又称框模型 (Box Model) ，包含了元素内容（content）、内边距（padding）、边框（border）、外边距（margin）几个要素。
2. 盒子模型 = margin + border + padding + content

```php+HTML
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>菜鸟教程(runoob.com)</title>
<style>
div {
    background-color: lightgrey;
    width: 300px;
    border: 25px solid green;	/* 25px 绿色边框 */
    padding: 25px;				/* 25px 内间距 */
    margin: 25px;				/* 25px 外间距 */
}
</style>
</head>
<body>

<h2>盒子模型演示</h2>

<p>CSS盒模型本质上是一个盒子，封装周围的HTML元素，它包括：边距，边框，填充，和实际内容。</p>

<div>这里是盒子内的实际内容。有 25px 内间距，25px 外间距、25px 绿色边框。</div>

</body>
</html>
```

**box-sizing 属性介绍**

box-sizing 属性是用户界面属性里的一种，之所以介绍它，是因为这个属性跟盒子模型有关，而且在 css reset 中有可能会用到它。

box-sizing : content-box|border-box|inherit;

(1) content-box ,默认值，可以使设置的宽度和高度值应用到元素的内容框。盒子的 width 只包含内容。

即总宽度=margin+border+padding+width

(2) border-box , 设置的 width 值其实是除 margin 外的 border+padding+element 的总宽度。盒子的 width 包含 border+padding+内容

即总宽度=margin+width

很多 CSS 框架，都会对盒子模型的计算方法进行简化。

(3) inherit , 规定应从父元素继承 box-sizing 属性的值

关于 border-box 的使用：

1 一个 box 宽度为 100%，又想要两边有内间距，这时候用就比较好
2 全局设置 border-box 很好，首先它符合直觉，其次它可以省去一次又一次的加加减减，它还有一个关键作用——让有边框的盒子正常使用百分比宽度。

**实际开发中遇到的和框模型相关的应用及小问题。**

1. margin 越界（第一个子元素的 margin-top 和最后一个子元素的 margin-bottom 的越界问题）

以第一个子元素的 margin-top 为例：

当父元素没有边框 border 时，设置第一个子元素的 margin-top 值的时候，会出现 margin-top 值加在父元素上的现象，解决方法有四个：

（1）给父元素加边框 border （副作用）

（2）给父元素设置 padding 值 （副作用）

（3）父元素添加 overflow：hidden （副作用）

（4）父元素加前置内容生成。（推荐）

```html
<style>
	.parent {
		width: 500px;
		height: 500px;
		background-color: red;
	}
	.parent: before {
		content: " ";
		display: table;
	}

	.child {
		width: 200px;
		height: 200px;
		background-color: green;
		margin-top: 50px;
	}
</style>
<div class="parent">
	<div class="child"></div>
</div>
```

2. 浏览器间的盒子模型。

（1）ul 标签在 Mozilla 中默认是有 padding 值的，而在 IE 中只有 margin 有值。

（2）标准盒子模型与 IE 模型之间的差异：

标准的盒子模型就是上述介绍的那种，而 IE 模型更像是 box-sizing : border-box; 其内容宽度还包含了 border 和 padding。解决办法就是：在 html 模板中加 doctype 声明。

### 8. CSS 边框

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>菜鸟教程(runoob.com)</title>
		<style>
			p {
				border-style: solid dotted solid; /* 上(top)、右(right)、下(bottom)、左(left)(若不满四个相对的是什么，就是什么) */
			}
		</style>
	</head>

	<body>
		<p>两个不同的边界样式。</p>
	</body>
</html>
```

### 9. CSS 轮廓（outline）属性

| 属性                                                                 | 说明                           | 值                                                                  | CSS |
| :------------------------------------------------------------------- | :----------------------------- | :------------------------------------------------------------------ | :-- |
| [outline](https://www.runoob.com/cssref/pr-outline.html)             | 在一个声明中设置所有的轮廓属性 | `*outline-color outline-style outline-width *inherit`               | 2   |
| [outline-color](https://www.runoob.com/cssref/pr-outline-color.html) | 设置轮廓的颜色                 | `*color-name hex-number rgb-number *invert inherit`                 | 2   |
| [outline-style](https://www.runoob.com/cssref/pr-outline-style.html) | 设置轮廓的样式                 | `none dotted dashed solid double groove ridge inset outset inherit` | 2   |
| [outline-width](https://www.runoob.com/cssref/pr-outline-width.html) | 设置轮廓的宽度                 | `thin medium thick *length *inherit`                                | 2   |

### 10. CSS position

1. relative 与 absolute 的主要区别
    1. 在正常流中的位置存在与否
    2. relative 定位的层总是相对于其最近的父元素，无论其父元素是何种定位方式。
2. 对于 absolute 定位的层总是相对于其最近的定义为 absolute 或 relative 的父层，而这个父层并不一定是其直接父层。如果其父层中都未定义 absolute 或 relative，则其将相对 body 进行定位。

| 值       | 描述                                                         |
| :------- | :----------------------------------------------------------- |
| absolute | 生成绝对定位的元素，相对于 **static 定位以外的第一个父元素**进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。<br />若想把一个定位属性为`absolute`的元素定位于其父级元素内，只有满足两个条件：第一：设定`TRBL`（"top", "right", "bottom", "left"）；第二：父级设定`Position`属性。<br />`Top`的值表示对象上边框与浏览器窗口顶部的距离，`bottom`的值表示对象下边框与浏览器窗口底部的距离，两者同时存在时，只有`Top`起作用；如果两者都未指定，则其顶端将与原文档流位置一致，即垂直保持位置不变。<br />`left`的值表示对象左边框与浏览器窗口左边的距离，`right`的值表示对象右边框与浏览器窗口右边的距离，两者同时存在时，只有`left`起作用；如果两者都未指定，则其左边将与原文档流位置一致，即水平保持位置不变。<br />在`Position`属性值为`absolute`的同时，如果有一级父对象（无论是父对象还是祖父对象，或者再高的辈分，一样）的`Position`属性值为`relative`时，则上述的相对浏览器窗口定位将会变成相对父对象定位，这对精确定位是很有帮助的。<br />属性为`relative`的元素可以用来布局页面，属性为`absolute`的元素用来定位某元素在父级中的位置，既然属性为`absolute`的元素用来定位某元素在父级中位置，就少不了 TRBL，这时候根据一开始讲的`absolute`的第三条，如果父级元素没有`position`属性那么 `absolute`元素就会脱离父级元素，但是如果是布局页面，父级元素`position`的属性又不能为`absolute`，不然就会以浏览器左上角为原点 了，**所以父级元素的`position`属性只能为`relative`！**<br>绝对定位不再占有原先的位置（**脱标**）。 |
| fixed    | 生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定。 |
| relative | 生成相对定位的元素，相对于其正常位置（**原来的位置**）进行定位。因此，"left:20" 会相对其原来的位置向元素的 `left`位置添加 20 像素。所以 `relative` 又称为自恋型定位<br />无论父级存在不存在，无论有没有 trbl（top、right、bottom、left），均是以父级的左上角进行定位，但是父级的`Padding`属性会对其影响。<br />`Top`的值表示对象相对原位置向下偏移的距离，`bottom`的值表示对象相对原位置向上偏移的距离，两者同时存在时，只有`Top`起作用。<br />`left`的值表示对象相对原位置向右偏移的距离，`right`的值表示对象相对原位置向左偏移的距离，两者同时存在时，只有`left`起作用。<br>原来在标准流的位置会继续占有，后面的盒子仍然以标准流的方式对待它。（**不脱标，继续保留原来的位置**） |
| static   | 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right 或者 z-index 声明）。 |
| inherit  | 规定应该从父元素继承 position 属性的值。                     |

### 11. 后台管理系统界面设计

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<meta name="viewport" content="width=device-width, initial-scale=1.0" />
		<title>Document</title>
		<style>
			body {
				margin: auto;
			}
			.pg-header {
				background-color: turquoise;
				height: 48px;
			}
			.pg-body .body-menu {
				position: absolute;
				top: 48px;
				left: 0px;
				bottom: 0px;
				width: 200px;
				background-color: rgb(150, 174, 238);
			}
			/* 样式一：
        .pg-body .body-content{
            position: absolute;
            top: 48px;
            left: 210px;
            right: 0px;
            background-color: rgb(213, 150, 238);
        } */
			/* 样式二： */
			.pg-body .body-content {
				position: absolute;
				top: 48px;
				left: 210px;
				bottom: 0px;
				right: 0px;
				background-color: rgb(213, 150, 238);
				overflow: auto;
			}
		</style>
	</head>
	<body>
		<div class="pg-header"></div>
		<div class="pg-body">
			<div class="body-menu"></div>
			<div class="body-content">
				frijol;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />
				fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />
				fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />
				fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />
				fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />
				fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />fghjkl;<br />
			</div>
		</div>
		<div class="pg-bottom"></div>
	</body>
</html>
```

### 12. 网站布局方式

#### 1. 网页布局方式：

1、固定宽度布局：为网页设置一个固定的宽度，通常以 px 做为长度单位，常见于 PC 端网页。

2、流式布局：为网页设置一个相对的宽度，通常以百分比做为长度单位。

3、栅格化布局：将网页宽度人为的划分成均等的长度，然后排版布局时则以这些均等的长度做为度量单位，通常利用百分比做为长度单位来划分成均等的长度。

4、响应式布局：通过检测设备信息，决定网页布局方式，即用户如果采用不同的设备访问同一个网页，有可能会看到不一样的内容，一般情况下是检测设备屏幕的宽度来实现。

注：以上几种布局方式并不是独立存在的，实际开发过程中往往是相互结合使用的。

#### 2. 响应式布局

1. Responsive design，意在实现不同屏幕分辨率的终端上浏览网页的不同展示方式。通过响应式设计能使网站在手机和平板电脑上有更好的浏览阅读体验。屏幕尺寸不一样展示给用户的网页内容也不一样，我们利用媒体查询可以检测到屏幕的尺寸（主要检测宽度），并设置不同的 CSS 样式，就可以实现响应式的布局。
2. 我们利用响应式布局可以满足不同尺寸的终端设备非常完美的展现网页内容，使得用户体验得到了很大的提升，但是为了实现这一目的我们不得不利用媒体查询写很多冗余的代码，使整体网页的体积变大，应用在移动设备上就会带来严重的性能问题。
3. 响应式布局常用于企业的官网、博客、新闻资讯类型网站，这些网站以浏览内容为主，没有复杂的交互。

#### 3. 响应式开发的原理：媒体查询：

**查询媒介，查询到当前屏幕(媒介媒体)的宽度，针对不同的屏幕宽度设置不同的样式来适应不同屏幕**。当你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面。简单说，你可以设置 不同屏幕下面的不同的样式，达到适配不同的屏幕的目的。

**实现方式**：通过查询 screen 的宽度来指定某个宽度区间的网页布局。

-   超小屏幕 （移动设备） w<768px
-   小屏设备 768px-992px 768 <= w <992
-   中等屏幕 992px-1200px 992 =< w <1200
-   宽屏设备 1200px 以上 w>=1200

**CSS 语法**

```css
@media mediatype and|not|only (media feature) {
    CSS-Code;
}
```

也可以针对不同的媒体使用不同 stylesheets :

```html
<link rel="stylesheet" media="mediatype and|not|only (media feature)" href="mystylesheet.css" />
```

**媒体类型**

| 值     | 描述                                 |
| :----- | :----------------------------------- |
| all    | 用于所有设备                         |
| print  | 用于打印机和打印预览                 |
| screen | 用于电脑屏幕，平板电脑，智能手机等。 |
| speech | 应用于屏幕阅读器等发声设备           |

**媒体功能**

| 值                | 描述                                   |
| :---------------- | :------------------------------------- |
| device-height     | 定义输出设备的屏幕可见高度。           |
| device-width      | 定义输出设备的屏幕可见宽度。           |
| max-device-height | 定义输出设备的屏幕可见的最大高度。     |
| max-device-width  | 定义输出设备的屏幕最大可见宽度。       |
| min-device-width  | 定义输出设备的屏幕最小可见宽度。       |
| min-device-height | 定义输出设备的屏幕的最小可见高度。     |
| max-height        | 定义输出设备中的页面最大可见区域高度。 |
| max-width         | 定义输出设备中的页面最大可见区域宽度。 |
| min-height        | 定义输出设备中的页面最小可见区域高度。 |
| min-width         | 定义输出设备中的页面最小可见区域宽度。 |

### 13. CSS 过渡、动画和变换

#### 1. **CSS 过渡（transition）**

| 属性                       | 说明                                   |
| -------------------------- | -------------------------------------- |
| transition-delay           | 指定过渡开始之前的延时时间             |
| transition-duration        | 指定过渡的持续时间                     |
| transition-property        | 指定应用过渡的属性                     |
| transition-timing-function | 指定过渡期间计算中间值的方式           |
| transition                 | 在一条声明中指定所有过渡细节的简写属性 |

`transition-delay` 和 `transition-duration` 属性指定为 CSS 时间，是一个数字，单位为 ms（毫秒）或者 s（秒）。
`transition`简写属性的格式如下：

```css
transition: <transition-property> <transition-duration> <transition-timing-function>
	<transition-delay>;
```

使用过渡时，浏览器需要为每个属性计算初始值和最终值之间的中间值。使用`transition-timing-function` 属性指定计算中间值的方式，表示为四个点控制的三次贝塞尔曲线。有五种预设曲线可以选择，由下面的值表示：

-   ease（默认值）：逐渐放慢
-   linear：匀速
-   ease-in：加速
-   ease-out：减速
-   ease-in-out：先加速后减速

*   cubic-bezier 函数：自定义速度模式（可以使用[工具网站](http://cubic-bezier.com/)来定制。）
    **transition 的使用注意**
*   目前，各大浏览器（包括 IE 10）都已经支持无前缀的 `transition`，所以 `transition` 已经可以很安全地不加浏览器前缀。
*   不是所有的 CSS 属性都支持 `transition`，完整的列表查看[这里](http://oli.jp/2010/css-animatable-properties/)，以及具体的[效果](http://leaverou.github.io/animatable/)。
*   `transition`需要明确知道，开始状态和结束状态的具体数值，才能计算出中间状态。比如，height 从 0px 变化到 100px，`transition`可以算出中间状态。但是，`transition`没法算出 0px 到 auto 的中间状态，也就是说，如果开始或结束的设置是`height: auto`，那么就不会产生动画效果。类似的情况还有，`display: none 到 block`，`background: url(foo.jpg)到url(bar.jpg)`等等。
    **transition 的局限**
    transition 的优点在于简单易用，但是它有几个很大的局限。
*   transition 需要事件触发，所以没法在网页加载时自动发生。
*   transition 是一次性的，不能重复发生，除非一再触发。
*   transition 只能定义开始状态和结束状态，不能定义中间状态，也就是说只有两个状态。
*   一条 transition 规则，只能定义一个属性的变化，不能涉及多个属性。
    CSS Animation 就是为了解决这些问题而提出的。

#### 2. **CSS 动画（Animation）**

CSS 动画本质上是增强的过渡。在如何从一种样式过渡到另一种样式的过程中，具有了更多选择、更多控制，以及更多灵活性。
| 属性 | 说明 | 值 |
| ------------------------- | ---------------------------------------- | ------------------------------------------------------------------ |
| animation-delay | 设置动画开始前的延迟 | < 时间 > |
| animation-direction | 设置动画循环播放的时候是否反向播放 | normal（正常的）、alternate（反向）、reverse、alternate-reverse 等 |
| animation-duration | 设置动画播放的持续时间 | < 时间 > |
| animation-iteration-count | 设置动画的播放次数 | infinite(无限)、< 数值 > |
| animation-name | 指定动画名称 | none、< 字符串 > |
| animation-play-state | 允许动画暂停和重新播放 | running、paused |
| animation-timing-function | 指定如何计算中间动画值 | ease、linear、ease-in、ease-out、ease-in-out、cubic-bezier |
| animation-fill-mode | 动画在播放之前或之后，其动画效果是否可见 | none、forwards、backwards、both |
| animation | 简写属性 | |
animation 简写属性的格式如下：

```css
animation: <animation-name> <animation-duration> <animation-timing-function> <animation-delay>
	<animation-iteration-count>;
```

注意，这些属性都不是用来指定要作为动画的 CSS 属性的。这是因为动画是在两部分定义的。第一部分包含在样式声明中，使用了上面表中列出的属性。它们定义了动画的样式，但并没有定义哪些属性是动画。第二部分使用 `@keyframes` 规则窗口，用来定义定义动画的属性。

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<title>z-index</title>
		<style>
			div {
				position: absolute;
			}
			#container div {
				background-color: lightblue;
				border: 1px solid #333333;
				width: 100px;
				height: 100px;
				opacity: 0.5;
			}
			div #myBox {
				opacity: 1;
				background-color: coral;
				z-index: 1;
				/* 动画名 播放一次动画的时间 无限播放 线性播放 */
				-webkit-animation: myMove 5s infinite linear;
				/* Chrome, Safari, Opera */
				animation: myMove 5s infinite linear;
			}
			/* Chrome, Safari, Opera */
			@-webkit-keyframes myMove {
				/* 表示在第2.5s的时候 z-index 的值达到5 */
				50% {
					z-index: 5;
				}
			}
			/* Standard syntax */
			@keyframes myMove {
				50% {
					z-index: 5;
				}
			}
		</style>
	</head>
	<body style="position:absolute">
		<p>z-index 属性支持动画效果。</p>
		<p><b>注意：</b>Internet Explorer 9 及更早 IE 版本不支持 CSS 动画。</p>
		<p>逐步改变 "myBox" 的 z-index 属性 从 1 到 5:</p>
		<p></p>
		<div id="container">
			<div id="myBox">myBox</div>
			<div style="top:20px;left:20px;z-index:1;">z-index 1</div>
			<div style="top:40px;left:40px;z-index:2;">z-index 2</div>
			<div style="top:60px;left:60px;z-index:3;">z-index 3</div>
			<div style="top:80px;left:80px;z-index:4;">z-index 4</div>
		</div>
		<div id="demo"></div>
		<script>
			var myVar = setInterval(myTimer, 1000)
			function myTimer() {
				var d = new Date()
				document.getElementById("demo").innerHTML = d.toLocaleTimeString()
			}
		</script>
	</body>
</html>
```

上面的

```css
@-webkit-keyframes myMove {
	/* 表示在第2.5s的时候 z-index 的值达到5 */
	50% {
		z-index: 5;
	}
}
```

等价于：

```css
@-webkit-keyframes myMove {
	0% {
		z-index: 1;
	}
	50% {
		z-index: 5;
	}
	100% {
		z-index: 1;
	}
}
```

**`animation-fill-mode` 详解：**
动画结束以后，会立即从结束状态跳回到起始状态。如果想让动画保持在结束状态，需要使用 `animation-fill-mode` 属性。

```css
animation-fill-mode: none | forwards | backwards | both;
```

| 值        | 描述                                                                                              |
| :-------- | :------------------------------------------------------------------------------------------------ |
| none      | 不改变默认行为。                                                                                  |
| forwards  | 当动画完成后，保持最后一个属性值（在最后一个关键帧中定义）。                                      |
| backwards | 在 animation-delay 所指定的一段时间内，在动画显示之前，应用开始属性值（在第一个关键帧中定义）。   |
| both      | 向前和向后填充模式都被应用。根据 animation-direction（见后）轮流应用 forwards 和 backwards 规则。 |

**`animation-direction` 详解：**
动画循环播放时，每次都是从结束状态跳回到起始状态，再开始播放。animation-direction 属性，可以改变这种行为。
下面看一个例子，来说明如何使用 animation-direction。假定有一个动画是这样定义的。

```css
@keyframes rainbow {
	0% {
		background-color: yellow;
	}
	100% {
		background: blue;
	}
}
```

默认情况是，animation-direction 等于 normal。

```css
div:hover {
	animation: 1s rainbow 3 normal;
}
```

此外，还可以等于取 alternate、reverse、alternate-reverse 等值。它们的含义见下图（假定动画连续播放三次）。
![img](.\笔记图片\bg2014021401.png)
简单说，`animation-direction` 指定了动画播放的方向，最常用的值是 `normal` 和 `reverse` 。浏览器对其他值的支持情况不佳，应该慎用。
**animation 的各项属性**
同 transition 一样，animation 也是一个简写形式。

```css
div:hover {
	animation: 1s 1s rainbow linear 3 forwards normal;
}
```

这是一个简写形式，可以分解成各个单独的属性。

```css
div:hover {
	animation-name: rainbow;
	animation-duration: 1s;
	animation-timing-function: linear;
	animation-delay: 1s;
	animation-fill-mode: forwards;
	animation-direction: normal;
	animation-iteration-count: 3;
}
```

**keyframes 的写法：**
keyframes 关键字用来定义动画的各个状态，它的写法相当自由。

```css
@keyframes rainbow {
	0% {
		background: #c00;
	}
	50% {
		background: orange;
	}
	100% {
		background: yellowgreen;
	}
}
```

0%可以用 from 代表，100%可以用 to 代表，因此上面的代码等同于下面的形式。

```css
@keyframes rainbow {
	from {
		background: #c00;
	}
	50% {
		background: orange;
	}
	to {
		background: yellowgreen;
	}
}
```

如果省略某个状态，浏览器会自动推算中间状态，所以下面都是合法的写法。

```css
@keyframes rainbow {
	50% {
		background: orange;
	}
	to {
		background: yellowgreen;
	}
}
@keyframes rainbow {
	to {
		background: yellowgreen;
	}
}
```

甚至，可以把多个状态写在一行。

```css
@keyframes pound {
	from，to {
		transform: none;
	}
	50% {
		transform: scale(1.2);
	}
}
```

另外一点需要注意的是，浏览器从一个状态向另一个状态过渡，是平滑过渡。steps 函数可以实现分步过渡。

```css
div:hover {
	animation: 1s rainbow infinite steps(10);
}
```

**初始布局时应用动画：**
跟过渡相比，动画的一个优势是可以将其应用到页面的初始布局。当把 `animation-delay` 属性的值设为 0 （默认值），当页面一旦加载就会自动应用样式，这就意味着浏览器一旦显示 HTML 就有了动画效果。
PS:使用上诉方法要谨慎。如果要在页面中使用动画，而动画效果不是邀请用户只需某一动作，这种情况更应该慎之又慎。如果确实要使用动画，要保证动画效果缓和一些，不要妨碍用户阅读或者与页面其他部分交互。
**浏览器前缀：**
目前，IE 10 和 Firefox（>= 16）支持没有前缀的 animation，而 chrome 不支持，所以必须使用 webkit 前缀。
也就是说，实际运用中，代码必须写成下面的样子：

```css
div:hover {
	-webkit-animation: 1s rainbow;
	animation: 1s rainbow;
}
@-webkit-keyframes rainbow {
	0% {
		background: #c00;
	}
	50% {
		background: orange;
	}
	100% {
		background: yellowgreen;
	}
}
@keyframes rainbow {
	0% {
		background: #c00;
	}
	50% {
		background: orange;
	}
	100% {
		background: yellowgreen;
	}
}
```

#### 3. CSS 变换（transform）：

我们可以使用 CSS 变换为元素应用线性变换，也就是说可以旋转、缩放、倾斜和平移某个元素。
| 属性 | 值 |
| ---------------- | ------------------ |
| transform | 指定应用的变换功能 |
| transform-origin | 指定变换的起点 |
**3.1 应用变换**
![img](.\笔记图片\940966-20160721162239357-1648666965.png)
下面代码是一个变换的例子。

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>Example</title>
		<style type="text/css">
			img {
				border: medium double green;
				background-color: lightgray;
			}
			#banana2 {
				transform: rotate(-45deg) scaleX(1.2);
			}
		</style>
	</head>
	<body>
		<p>
			<img src="imgs/banana-small.png" alt="small banana" id="banana1" />
		</p>
		<p>
			<img src="imgs/banana-small.png" alt="small banana" id="banana2" />
		</p>
	</body>
</html>
```

    此例中，为#banana2 选择器添加了一个transform 属性声明，指定了两个变换。第一个是旋转-45°（即逆时针旋转45°）；第二个是沿x轴进行因子为1.2的缩放。这些变换的效果如下图所示：

**3.2 指定元素变换的起点**
transform-origin 属性允许我们指定应用变换的起点。默认情况下，使用元素的中心作为起点，不过，可以使用下表中的值选择其他起点。
| 值 | 说明 |
| --------------------------- | ---------------------------- |
| < % > | 指定元素 x 轴或者 Y 轴的起点 |
| < 长度值 > | 指定距离 |
| left<br />center<br />right | 指定 x 轴上的距离 |
| top<br />center<br />bottom | 指定 Y 轴上的距离 |
要定义起点，需要为 x 轴和 y 轴各定义一个值。如果只提供一个值，另一个值会被认为是中心位置。下面代码展示了 transform-origin 属性的用法。

```html
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="UTF-8" />
		<title>Example</title>
		<style type="text/css">
			img {
				border: medium double green;
				background-color: lightgray;
			}
			#banana2 {
				transform: rotate(-45deg) scaleX(1.2);
				transform-origin: right top;
			}
		</style>
	</head>
	<body>
		<p>
			<img src="imgs/banana-small.png" alt="small banana" id="banana1" />
		</p>
		<p>
			<img src="imgs/banana-small.png" alt="small banana" id="banana2" />
		</p>
	</body>
</html>
```

此例中，将变换的起点已到了元素的右上角。
**3.3 将变换作为动画和过渡处理**
我们可以为变换应用动画和过渡，就和其他 CSS 属性一样。

```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Example</title>
    <style type="text/css">
        img{ border: medium double green; background-color: lightgray;}
        #banana2:hover {
            transform: rotate(360deg);
            transition-duration: 5s;
        }
    </style>
</head>
<body>
<p>
<img src="imgs/banana-small.png" alt="small banana" id="banana1"></p>
<p>
<img src="imgs/banana-small.png" alt="small banana" id="banana2"></p>
</body>
</html>
```

此例中，定义了一个过渡，它会经过 5 秒完成一次 360° 旋转变换。当用户将鼠标悬停在 #banana2 元素上，就会应用过渡。

### 14. `display` 详解

1. `display` 介绍

    `display` 属性设置元素是否被显示

2. 标准文档流的组成

    1. 块级元素（block）：<h1>…<h6>、<p>、<div>、列表

        - `block`元素会独占一行，多个`block`元素会各自新起一行。默认情况下，`block`元素宽度自动填满其父元素宽度
        - `block`元素可以设置`width`和`height`属性。块级元素即使设置了宽度,仍然是独占一行
        - `block`元素也可以设置`margin`和`padding`属性
        - `block`是一个容器及盒子，里面可以放行内元素和块级元素
        - 注意：
            - 文字类元素内不能使用块级元素
            - `<p>`标签主要用于存放文字，因此`<p>`里面不能放块级元素，特别是不能放`<div>`，`<h1> - <h6>` 也是如此。

    2. 内联元素（行内元素）（inline）：<span>、<a>、<img/>、<strong>...

        - `inline`元素不会独占一行，多个相邻的行内元素会排列在同一行里，直到一行排列不下，才会新换一行
        - `inline`元素默认的宽度是自身内容的宽度(默认有多少占多少)
        - `inline`元素设置`width`和`height`属性**无效**
            - `inline`元素的`margin`和`padding`属性，水平方向的`padding-left`, `padding-right`, `margin-left`, `margin-right`都**产生**边距效果；但竖直方向的`padding-top`, `padding-bottom`, `margin-top`, `margin-bottom`**不会产生**边距效果。
        - `inline`元素只能容纳文本或其他行内元素
            - `<a>` 元素里面不能再存放 `<a>` 元素，但是可以存放块元素。

    3. 行内块元素（inline-block）：

        简单来说就是将对象呈现为`inline`对象，但是对象的内容作为`block`对象呈现。之后的内联对象会被排列在同一行内。比如我们可以给一个`link`（a 元素）设置`inline-block`属性，使其既具有`block`的可设置宽度和高度特性又具有`inline`的同行特性

        注：内联标签可以包含于块级标签中，成为它的子元素，而反过来则不成立

        例如：h1 中可以嵌套 span 元素，但是 span 中不能嵌套 h1 元素

3. `display` 属性

    | 值                 | 描述                                                             |
    | :----------------- | :--------------------------------------------------------------- |
    | none               | 此元素不会被显示。                                               |
    | block              | 此元素将显示为块级元素，此元素前后会带有换行符。                 |
    | inline             | 默认。此元素会被显示为内联元素，元素前后没有换行符。             |
    | inline-block       | 行内块元素。（CSS2.1 新增的值）                                  |
    | list-item          | 此元素会作为列表显示。                                           |
    | run-in             | 此元素会根据上下文作为块级元素或内联元素显示。                   |
    | compact            | CSS 中有值 compact，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。 |
    | marker             | CSS 中有值 marker，不过由于缺乏广泛支持，已经从 CSS2.1 中删除。  |
    | table              | 此元素会作为块级表格来显示（类似 <table>），表格前后带有换行符。 |
    | inline-table       | 此元素会作为内联表格来显示（类似 <table>），表格前后没有换行符。 |
    | table-row-group    | 此元素会作为一个或多个行的分组来显示（类似 <tbody>）。           |
    | table-header-group | 此元素会作为一个或多个行的分组来显示（类似 <thead>）。           |
    | table-footer-group | 此元素会作为一个或多个行的分组来显示（类似 <tfoot>）。           |
    | table-row          | 此元素会作为一个表格行显示（类似 <tr>）。                        |
    | table-column-group | 此元素会作为一个或多个列的分组来显示（类似 <colgroup>）。        |
    | table-column       | 此元素会作为一个单元格列显示（类似 <col>）                       |
    | table-cell         | 此元素会作为一个表格单元格显示（类似 <td> 和 <th>）              |
    | table-caption      | 此元素会作为一个表格标题显示（类似 <caption>）                   |
    | inherit            | 规定应该从父元素继承 display 属性的值。                          |

    `display: block;`：显示为块元素，能让行内元素显示宽高，能让行内元素具有块元素的特征；

    `display: inline; `：显示为行内元素，能让块元素具有行内元素的特征；

    `display: inline-block;`：吸取行内元素和块元素共同的特征，既能排在一行，又能显示宽高；

    `display: none;`：元素在页面上看不见，隐藏了，但是在源代码中依然存在。

    `display: none;`可做列表布局，其中的类似于图片间的间隙小 bug 可以通过如下设置解决：

    ```css
    #outer {
    	border: 3px dashed;
    	word-spacing: -6px;
    }
    ```

### 15. CSS 命名规则

| CSS 样式命名           | 说明                     |
| ---------------------- | ------------------------ |
| 网页公共命名           |                          |
| #wrapper               | 页面外围控制整体布局宽度 |
| #container 或#content  | 容器,用于最外层          |
| #layout                | 布局                     |
| #head, #header         | 页头部分                 |
| #foot, #footer         | 页脚部分                 |
| #nav                   | 主导航                   |
| #subnav                | 二级导航                 |
| #menu                  | 菜单                     |
| #submenu               | 子菜单                   |
| #sideBar               | 侧栏                     |
| #sidebar_a, #sidebar_b | 左边栏或右边栏           |
| #main                  | 页面主体                 |
| #tag                   | 标签                     |
| #msg #message          | 提示信息                 |
| #tips                  | 小技巧                   |
| #vote                  | 投票                     |
| #friendlink            | 友情连接                 |
| #title                 | 标题                     |
| #summary               | 摘要                     |
| #loginbar              | 登录条                   |
| #searchInput           | 搜索输入框               |
| #hot                   | 热门热点                 |
| #search                | 搜索                     |
| #search_output         | 搜索输出和搜索结果相似   |
| #searchBar             | 搜索条                   |
| #search_results        | 搜索结果                 |
| #copyright             | 版权信息                 |
| #branding              | 商标                     |
| #logo                  | 网站 LOGO 标志           |
| #siteinfo              | 网站信息                 |
| #siteinfoLegal         | 法律声明                 |
| #siteinfoCredits       | 信誉                     |
| #joinus                | 加入我们                 |
| #partner               | 合作伙伴                 |
| #service               | 服务                     |
| #regsiter              | 注册                     |
| arr/arrow              | 箭头                     |
| #guild                 | 指南                     |
| #sitemap               | 网站地图                 |
| #list                  | 列表                     |
| #homepage              | 首页                     |
| #subpage               | 二级页面子页面           |
| #tool, #toolbar        | 工具条                   |
| #drop                  | 下拉                     |
| #dorpmenu              | 下拉菜单                 |
| #status                | 状态                     |
| #scroll                | 滚动                     |
| .tab                   | 标签页                   |
| .left .right .center   | 居左、中、右             |
| .news                  | 新闻                     |
| .download              | 下载                     |
| .banner                | 广告条(顶部广告条)       |

CSS 命名规则

```
头：header
内容：content/container
尾：footer
导航：nav
侧栏：sidebar
栏目：column
页面外围控制整体布局宽度：wrapper
左右中：left right center
登录条：loginbar
标志：logo
广告：banner
页面主体：main
热点：hot
新闻：news
下载：download
子导航：subnav
菜单：menu
子菜单：submenu
搜索：search
友情链接：friendlink
页脚：footer
版权：copyright
滚动：scroll
内容：content
标签页：tab
文章列表：list
提示信息：msg
小技巧：tips
栏目标题：title
加入：joinus
指南：guild
服务：service
注册：regsiter
状态：status
投票：vote
合作伙伴：partner
```

CSS+DIV 的命名规则：

```
登录条:loginBar
标志:logo
侧栏:sideBar
广告:banner
导航:nav
子导航:subNav
菜单:menu
子菜单:subMenu
搜索:search
滚动:scroll
页面主体:main
内容:content
标签页:tab
文章列表:list
提示信息:msg
小技巧:tips
栏目标题:title
友情链接:friendLink
页脚:footer
加入:joinus
指南:guild
服务:service
热点:hot
新闻:news
下载:download
注册:regsiter
状态:status
按钮:btn
投票:vote
合作伙伴:partner
版权:copyRight
```

1.CSSID 的命名

```
外套:wrap
主导航:mainNav
子导航:subnav
页脚:footer
整个页面:content
页眉:header
页脚:footer
商标:label
标题:title
主导航:mainNav(globalNav)
顶导航:topnav
边导航:sidebar
左导航:leftsideBar
右导航:rightsideBar
旗志:logo
标语:banner
菜单内容 1:menu1Content
菜单容量:menuContainer
子菜单:submenu
边导航图标:sidebarIcon
注释:note
面包屑:breadCrumb(即页面所处位置导航提示)
容器:container
内容:content
搜索:search
登陆:login
功能区:shop(如购物车，收银台)
当前的 current 2.样式文件命名
主要的:master.css
布局版面:layout.css
专栏:columns.css
文字:font.css
打印样式:print.css
主题:themes.css
```

### 16. CSS 选择器

1. 选择器权重

    1. 第一等：代表内联样式，如: style=””，权值为 1000。
    2. 第二等：代表 ID 选择器，如：#content，权值为 0100。
    3. 第三等：代表类，伪类和属性选择器，如.content，权值为 0010。
    4. 第四等：代表元素选择器和伪元素选择器，如 div p，权值为 0001。
    5. 通配符、子选择器、相邻选择器等的。如\*、>、+,权值为 0000。
    6. 继承的样式没有权值，相当于为 0。
    7. `!important`：权重为无穷大

    - 总结：important > 内联 > ID > 类 >伪类 | 属性选择 | 标签> 伪元素 > 通配符 > 继承

2. 权重叠加

    1. 如果是复合选择器，则会有权重叠加，需要重新计算。
    2. `div ul li` 的权重为：0,0,0,3
    3. `.nav ul li` 的权重为：0,0,1,2
    4. `a:hover` 的权重为：0,0,1,1（`:hover` 为 0,0,1,0）
    5. `.nav a` 的权重为：0,0,1,1

### 17. CSS 属性书写顺序

1. 布局定位属性：display、position、float、clear、visibility、overflow（建议 display 第一个写）
2. 自身属性：width、height、margin、padding、border、background
3. 文本属性：color、font、text-decoration、text-align、vertical-align、white-space、break-word
4. 其他属性（CSS3）：content、cursor、border-radius、text-shadow、background: linear-gradient ...

### 18. 导航栏制作注意点：

实际开发中，我们不会直接用链接<a>，而是用<li> 包含链接(`li + a`) 的做法。

1. `li + a` 语义更清晰，一看这就是有条理的列表型内容
2. 如果直接使用<a>，搜索引擎容易辨别为有堆砌关键字嫌疑（故意堆砌关键字容易被搜索引擎有降权的风险），从而影响网站排名

### 19. `vertical-align`

1. 使图片和文字居中对齐：`vertical-align: middle;`
2. 解决图片底部默认空白缝隙问题
    1. 原因：行内块元素会和文字的基线对齐
    2. 解决办法：给图片添加`vertical-align: middle | top | bottom;`

### 20. CSS3 盒子模型

1. CSS3 中可以用过`box-sizing`来指定盒模型，有两个值：即可指定为`content-box`、`border-box`，这样我们计算盒子大小的方式会发生改变

### 21. 外边距塌陷

1. 可以为父元素定义上边框
2. 可以为父元素定义上内边距
3. 可以为父元素添加`overflow: hidden;`

### 22. 网站 TDK 三大标签 SEO 优化

1. SEO（Search Engine Optimization）汉译为**搜索引擎优化**，是一种利用搜索引擎的规则提高网站在有关搜索引擎内自然排名的方式。

2. SEO 的目的是**对网站进行深度的优化**，从而帮助网站获取免费的流量，进而在搜索引擎上提升网站的排名，提高网站的知名度。

3. 页面必须有三个标签来符合 SEO 优化。

    1. title

        title 具有不可替代性，是我们内页的第一个重要的标签，是搜索引擎了解网页的入口和对网页主题归属的最佳判断点。

        建议：网站名（产品名）- 网站的介绍。

        ```HTML
        <title>品优购(PY.COM)-正品低价、品质保障、配送及时、轻松购物！</title>
        ```

    2. description

        简要说明网站主要是做什么的。

        ```HTML
        <meta name="description" content="品优购PY.COM-专业的综合网上购物商城,销售家电、数码通讯、电脑、家居百货、服装服饰、母婴、图书、食品等数万个品牌优质商品.便捷、诚信的服务，为您提供愉悦的网上购物体验!">
        ```

    3. keyword

        页面关键词，是搜索引擎的关注点之一。

        ```HTML
        <meta name="Keywords" content="网上购物,网上商城,手机,笔记本,电脑,MP3,CD,VCD,DV,相机,数码,配件,手表,存储卡,京东">
        ```

4. LOGO SEO 优化

    1. logo 里面首先要放一个`<h1>`标签，目的是为了提权，告诉搜索引擎，这个地方很重要。
    2. `<h1>`里面放一个链接，可以返回首页的，把 logo 的背景图片给链接即可。
    3. 为了搜索引擎收录我们，我们链接里面要放文字（网站名称），但是文字不要显示出来。
        1. 方法一：`text-indent` 移到盒子外面（text-indent: -9999px），然后 `overflow: hidden;` ，淘宝的做法。
        2. 方法二：直接给 `font-size: 0;`就看不到文字了，京东的做法。
    4. 最后给链接一个 title 属性，这样鼠标放在 logo 上就可以看到提示文字了。

### 23. 一般情况下，`<a>` 如果包含有宽度的盒子，`<a>` 需要转换为块级元素
