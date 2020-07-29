## Web中CSS的各种居中总结

### 前言

&nbsp;&nbsp;&nbsp;&nbsp;CSS中的居中分为**水平居中**和**垂直居中**，其中水平居中又分为**行内元素居中**和**块状元素居中**两种情况，而块状元素又分为**定宽块状元素居中**和**不定宽块状元素居中**。

### 一、水平居中

#### 1、行内元素居中

&nbsp;&nbsp;&nbsp;&nbsp;顾名思义，行内元素居中是只针对行内元素的，比如文本（text）、图片（img）、按钮等行内元素，可通过给父元素设置 `text-align: center` 来实现。另外，如果块状元素属性 `display: inline` 时，也可以使用该方法。
注：该方法对浮动元素 `float: right/left` 元素无效

```html
.div{
        text-align:center;
    }
<div class="div">Hello world</div>
```

#### 2、块状元素居中

（1）定宽块状元素居中
&nbsp;&nbsp;&nbsp;&nbsp;满足定宽（块状元素的宽度width为固定值）和块状两个条件的元素可以通过设置 `margin` 左右的值为 `auto` 实现居中。
&nbsp;&nbsp;&nbsp;&nbsp;注：该方法对浮动元素 `float: right/left` 和绝对定位 `position: absolute` 元素无效

```html
.div{
　　　　 width:200px;
　　　　 border:1px solid red;
        margin:0 auto;
    }
<div class="div">Hello world</div>
```

（2）不定宽块状元素居中
&nbsp;&nbsp;&nbsp;&nbsp;在实际工作中我们会遇到需要为“不定宽度的块状元素”设置居中，比如网页上的分页导航，因为分页的数量是不确定的，所以我们不能通过设置宽度来限制它的弹性。(不定宽块状元素：块状元素的宽度width不固定。)

##### 方法1：

&nbsp;&nbsp;&nbsp;&nbsp;将要显示的元素加入到 `table` 标签当中，然后为 `table` 标签设置 `margin: 0 auto;`来实现居中； 或者先使用 `display : table;`；再设该元素 `margin: 0 auto;` 来实现居中。若使用后面的`display: table;`方法会更简洁。

为什么加入table标签? 
&nbsp;&nbsp;&nbsp;&nbsp;加入table标签是利用table标签的长度自适应性——即不定义其长度也不默认父元素body的长度（table其长度根据其内文本长度决定），因此可以看做一个定宽度块元素，然后再利用定宽度块状居中的margin的方法，使其水平居中。

```html
.div1 {
    width: 500px;
    height: 100px;
    background-color: #ccc;
}
.table1 {
    height: 100px;
    margin: auto;
    background-color: rgb(124, 74, 74);
}
.table1 ul {
	padding-left: 0;
}
.table1 td {
    text-align: center;/* 当行文字水平居中 */
    vertical-align: center;/* 文字垂直居中 */
}
<div class="div1">
    <table class="table1">
        <tbody>
            <tr>
                <td>
                    <div>Hello world</div>
                    <div>Hello world</div>
                </td>
            </tr>
        </tbody>
    </table>
</div>
```

```html
.content{
    background: #ccc;
    display: table;
    margin: 0 auto;
}
<div class="content">Hello world</div>
```

##### 方法2：

&nbsp;&nbsp;&nbsp;&nbsp;改变块级元素的 `display` 为 `inline` 类型（设置为 行内元素 显示），然后使用 `text-align: center` 来实现居中效果。

&nbsp;&nbsp;&nbsp;&nbsp;这种方法相比第一种方法的优势是不用增加无语义标签，但也存在着一些问题：它将块状元素的 `display` 类型改为 `inline`，变成了行内元素，所以少了一些功能，比如设定长度值（变成`inline-block`就可以设置宽高）。

```html
.div2 {
	text-align: center;
}
.div2 ul {
    list-style: none;
    margin: 0;
    padding: 0;
    display: inline-block;
}

<div class="div2">
    <ul>
        <li>Hello world</li>
        <li>Hello world</li>
    </ul>
</div>
```

##### 方法3

&nbsp;&nbsp;&nbsp;&nbsp;此方法是将父元素设置为`position: relative;`，通过此方法可以实现水平和垂直居中。

```html
.box {
    height: 200px;
    width: 200px;
    position: relative;
    border: 1px solid red;
    float: left;
}

.content-box1 {
    width: 50px;
    height: 50px;
    position: absolute;
    background-color: #ccc;
    top: 50%;
    left: 50%;
    margin-top: -25px;
    margin-left: -25px;
    /*  
    水平居中+垂直居中,父设置为position:relative;
    子设置为position:absolute;top:50%;left:50%;
    margin-top:-自身高度的一半;margin-left:-自身宽度的一半;
    top:50%;left:50%;表示子元素左上角为原点，将其移至中心位置
    margin-top: -25px;margin-left: -25px;便可使子中心移至父中心
    */
}

.content-box2 {
    width: 50px;
    height: 50px;
    position: absolute;
    background-color: #ccc;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    margin: auto;
    /*  
    水平居中+垂直居中,父设置为position:relative;
    子设置为position:absolute;top:0;left:0;right:0;bottom:0;margin:auto;
    top: 0;left: 0;right: 0;bottom: 0;表示距离上下左右为0，
    再使用margin:auto;达到居中效果
    */
}

.content-box3 {
    width: 50px;
    height: 50px;
    position: absolute;
    background-color: #ccc;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    /*  
    水平居中+垂直居中,父设置为position:relative;
    子设置为position:absolute;top:50%;left:50%;transform:translate(-50%,-50%); 
    translate(-50%,-50%) 作用是，往上（x轴）,左（y轴）移动自身长宽的 50%，以使其居于中心位置。
	此方式与第一种类似，但是与负margin-left和margin-top实现居中不同的是，
	margin-left必须知道自身的宽高，而 translate() 可以在不知道宽高的情况下进行居中，
	translate() 函数中的百分比是相对于自身宽高的百分比，所以能进行居中。
    */
}
<div class="box">
    <div class="content-box1"></div>
</div>
<div class="box">
    <div class="content-box2"></div>
</div>
<div class="box">
    <div class="content-box3"></div>
</div>
```

##### 方法4

&nbsp;&nbsp;&nbsp;&nbsp;此方法是将父元素设置为 `display: flex;`，`justify-content: center;`为水平居中，`align-items: center;`为垂直居中。

```html
.flex {
    height: 200px;
    width: 200px;
    display: flex;
    border: 1px solid red;
    justify-content: center;
    align-items: center;
}
<div class="flex">
    <div>Hello World!</div>
</div>
```



### 二、垂直居中

#### 1、单行文本

&nbsp;&nbsp;&nbsp;&nbsp;单行文字居中，只适用于一行文字的情况，`line-height = height`

```html
.content h2{
    margin:0;
    height:100px;
    line-height:100px;
}

<div class="content">
    <p>Hello world</p>
</div>
```

#### 2、多行文本

（1）使用插入 `table (包括tbody、tr、td)`标签，同时设置 `vertical-align: middle`。

```html
.div1 {
    width: 500px;
    height: 100px;
    background-color: #ccc;
}
.table1 {
    height: 100px;
    margin: auto;
    background-color: rgb(124, 74, 74);
}
.table1 ul {
	padding-left: 0;
}
.table1 td {
    text-align: center;/* 当行文字水平居中 */
    vertical-align: center;/* 文字垂直居中 */
}
<div class="div1">
    <table class="table1">
        <tbody>
            <tr>
                <td>
                    <div>Hello world</div>
                    <div>Hello world</div>
                </td>
            </tr>
        </tbody>
    </table>
</div>
```

（2）父设置为 `table` 元素,自己为 `table-cell` 元素， `vertical-align:middle;` 子垂直居中

```html
.content{
    height: 200px;
    background: #ccc;
    display: table-cell;
    vertical-align: middle;
}

<div class="content">
    <p>Hello world</p>
    <p>Hello world</p>
    <p>Hello world</p>
</div>
```

#### 3、弹性布局

`align-content`与`align-items`的区别：

1. `align-content`：居中对齐弹性盒的各项 <div> 元素

   CSS3弹性盒子之`align-items`属性定义flex子项在flex容器的当前行的侧轴（纵轴）方向上的对齐方式。

   ```css
   div{
       display:flex;
       align-items:center;
   }
   ```

   div 元素位于容器的中心。弹性盒子元素在该行的侧轴（纵轴）上居中放置。（如果该行的尺寸小于弹性盒子元素的尺寸，则会向两个方向溢出相同的长度）。