#### JavaScript基础知识学习笔记

#### 一、 编写代码

1. 存在形式：

   ```js
   <script src="js.js"></script>
   <script>
       alert('123456');
   </script>
   ```

2. 放置位置：

   - 为使网页加载速度更快，将js代码放置在body标签的底部位置。

3. 变量

   ```js
   var a = 123;	//局部变量
   a = 123;		//全局变量
   ```
   
4. 规则
   请使用 {} 来代替 new Object()
   请使用 "" 来代替 new String()
   请使用 0 来代替 new Number()
   请使用 false 来代替 new Boolean()
   请使用 [] 来代替 new Array()
   请使用 /()/ 来代替 new RegExp()
   请使用 function (){}来代替 new Function()

#### 二、预解析：

在ES6之前，变量使用`var`声明，会存在变量的预解析（函数也有预解析），ES6引了`let`和`const`。

基本类型是直接存储在栈内存中，而对象是存储在堆内存中，变量只是持有该**对象的地址**。

1. 预解析概念：

   1. **概念**：在当前作用域中，JavaScript代码执行之前，浏览器首先会默认的把所有带var和function声明的变量进行提前的声明或者定义。
   2. **声明**：var num; 告诉浏览器在全局作用域中有一个num变量了，如果一个变量只是声明了，但是没有赋值，默认值是undefined。
   3. **定义**：num = 12; 定义就是给变量进行赋值。

2. var声明的变量和function声明的函数在预解析的区别

   1. var声明的变量和function声明的函数在预解析的时候有区别，var声明的变量在预解析的时候只是提前的声明，**function声明的函数在预解析的时候会提前声明并且会同时定义**。也就是说var声明的变量和function声明的函数的区别是在声明的同时有没同时进行定义。

3. 全局作用域下带var和不带var的区别：

   1. 在全局作用域中声明变量带var可以进行预解析，所以在赋值的前面执行不会报错；声明变量的时候不带var的时候，不能进行预解析，所以在赋值的前面执行会报错。

4. 预解析中的一些机制

   1. 不管条件是否成立，都要把带`var`的进行提前的声明
      JavaScript进行预解析的时候，会忽略所有if条件，因为在ES6之前并没有块级作用域的概念。

   2. 只预解析 `=` 左边的，右边的是指针，不参与预解析
      声明变量的时候尽量使用var fn = ...的方式。

   3. 自执行函数，定义和执行一起完成
      自执行函数定义的那个function在全局作用域下不进行预解析，当代码执行到这个位置的时候，定义和执行一起完成了。

   4. return 下的代码依然会进行预解析
      函数体中return后面的代码，虽然不再执行了，但是需要进行预解析，return中的代码，都是我们的返回值，所以不进行预解析。

   5. 名字已经声明过了，不需要重新的声明，但是需要重新的赋值

      ```js
      fn(); // -> 2                                           
      function fn() {console.log(1);}  （预解析1）
      fn(); // -> 2
      var fn = 10; // -> fn = 10          （预解析2）
      fn(); // -> 10()  Uncaught TypeError: fn is not a function
      function fn() {console.log(2);}        （预解析2）
      fn();//不执行
      //分析以上代码：
      //1、首先 预解析的时候（预解析1）fn作为函数声明定义->（预解析2）fn前面已经声明所以此次不再声明->（预解析3）fn作为函数重新定义赋值地址（因为前面已经声明所以直接定义）。
      //2、然后 执行的时候前面两个fn()直接调用重新赋值的function fn() {console.log(2);}当遇到var fn= 10;时再次对fn进行赋值此时fn为Number类型，所以执行下一条语句的时候就会报错Uncaught TypeError: fn is not a function
      ```

      

#### 三、事件：

1. this 当前触发事件的标签
2. 全局事件绑定  window.onKeyDown = function(){}
3. event 包含时间相关内容
4. 默认事件
   - 自定义优先：a, form
   - 默认优先：checkbox
5. onclick="return false;"   表示返回的为false不执行之后的时事件。

#### 四、正则表达式：

1. 定义正则表达式
   - reg = /正则表达式/;
   - g：全局
   - i：不区分大小写
   - m：换行匹配
2. 利用正则表达式
   - reg.test(字符串)
   - reg.exec(字符串)
     - 全局
     - 非全局
3. 字符串的方法：
   - search：
   - match：
   - repalce：

#### 五、jQuery：

1. JavaScript 库

   1. JavaScript库：即 library，是一个封装好的特定的集合（方法和函数）。从封装一大堆函数的角度理解库，就是在这个库中，封装了很多预先定义好的函数在里面，比如动画animate、hide、show，比如获取元素等。
   2. 简单理解： 就是一个JS 文件，里面对我们原生js代码进行了封装，存放到里面。这样我们可以快速高效的使用这些封装好的功能了。
   3. 常见的JavaScript 库：jQuery、Prototype、YUI、Dojo、Ext JS、移动端的zepto等，这些库都是对原生 JavaScript 的封装，内部都是用 JavaScript 实现的，我们主要学习的是 jQuery。
   
2. jQuery的概念

   1. jQuery总体概况如下 :
      1. jQuery 是一个快速、简洁的 JavaScript 库，其设计的宗旨是“write Less，Do More”，即倡导写更少的代码，做更多的事情。
      2. j 就是 JavaScript；   Query 查询； 意思就是查询js，把js中的DOM操作做了封装，我们可以快速的查询使用里面的功能。
      3. jQuery 封装了 JavaScript 常用的功能代码，优化了 DOM 操作、事件处理、动画设计和 Ajax 交互。
      4. 学习jQuery本质： 就是学习调用这些函数（方法）。
      5. jQuery 出现的目的是加快前端人员的开发速度，我们可以非常方便的调用和使用它，从而提高开发效率。

3. jQuery的入口函数

   jQuery中常见的两种入口函数：

   ```js
   // 第一种: 简单易用。
   $(function () {   
       ...  // 此处是页面 DOM 加载完成的入口
   }) ; 
   
   // 第二种: 繁琐，但是也可以实现
   $(document).ready(function(){
      ...  //  此处是页面DOM加载完成的入口
   });
   ```

   1. 总结：
      1. 等着 DOM 结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完成，jQuery 帮我们完成了封装。
      2. 相当于原生 js 中的 DOMContentLoaded。
      3. 不同于原生 js 中的 load 事件是等页面文档、外部的 js 文件、css文件、图片加载完毕才执行内部代码。
      4. 更推荐使用第一种方式。

4. jQuery中的顶级对象$

   1. \$是 jQuery 的别称，在代码中可以使用 jQuery 代替，但一般为了方便，通常都直接使用 $ 。
   2. \$是jQuery的顶级对象，相当于原生JavaScript中的 window。把元素利用$包装成jQuery对象，就可以调用jQuery 的方法。

5.  jQuery 对象和 DOM 对象

   1. 使用 jQuery 方法和原生JS获取的元素是不一样的，总结如下 : 
      1. 用原生 JS 获取来的对象就是 DOM 对象
      2. jQuery 方法获取的元素就是 jQuery 对象。
      3. jQuery 对象本质是： 利用$对DOM 对象包装后产生的对象（伪数组形式存储）。
   2. 注意：
      1. 只有 jQuery 对象才能使用 jQuery 方法，DOM 对象则使用原生的 JavaScirpt 方法。

6. jQuery 对象和 DOM 对象转换

   1. DOM 对象与 jQuery 对象之间是可以相互转换的。因为原生js 比 jQuery 更大，原生的一些属性和方法 jQuery没有给我们封装. 要想使用这些属性和方法需要把jQuery对象转换为DOM对象才能使用。

      ```js
      // 1.DOM对象转换成jQuery对象，方法只有一种
      var box = document.getElementById('box');  // 获取DOM对象
      var jQueryObject = $(box);  // 把DOM对象转换为 jQuery 对象
      
      // 2.jQuery 对象转换为 DOM 对象有两种方法：
      //   2.1 jQuery对象[索引值]
      var domObject1 = $('div')[0]
      
      //   2.2 jQuery对象.get(索引值)
      var domObject2 = $('div').get(0)
      ```

   2. 总结：实际开发比较常用的是把DOM对象转换为jQuery对象，这样能够调用功能更加强大的jQuery中的方法。

7. 查找：

   1. 选择器
      
      1. 基础选择器
      
      | 名称       | 用法              | 描述                   |
      | ---------- | ----------------- | ---------------------- |
      | ID选择器   | `$('#id')`        | 获取指定ID元素         |
      | 全选择器   | `$('*')`          | 匹配所有元素           |
      | 类选择器   | `$('.class')`     | 获取同一类class的元素  |
      | 标签选择器 | `$('div')`        | 获取同一标签的所有元素 |
      | 并集选择器 | `$('div, p, li')` | 选取多个元素           |
      | 交集选择器 | `$('li.current')` | 交集元素               |
      
      2. 层级选择器
         1. 层级选择器最常用的两个分别为：后代选择器和子代选择器。
         2. 子选择器：`$("ul>li");` 使用 `>` 号，获取亲儿子层级的元素
         3. 后代选择器：`$("ul li");` 使用空格，代表后代选择器
      
   2. 筛选器
      - `$('i1').find('a')`		// 搜索所有与指定表达式匹配的元素。这个函数是找出正在处理的元素的后代元素的好方法。

      - `:eq(index)`					//匹配一个给定索引值的元素

        | 语法         | 用法            | 描述                                                         |
        | ------------ | --------------- | ------------------------------------------------------------ |
        | `:first`     | `$('li:first')` | 获取第一个li元素                                             |
        | `:last`      | `$('li:last')`  | 获取最后一个li元素                                           |
        | `:eq(index)` | `$('li:eq(2)')` | 获取到的li元素中，选择索引号为 index 的元素，index 从 0  开始 |
        | `:odd`       | `$('li:odd')`   | 获取到的li元素中，选择索引号为奇数的元素                     |
        | `:even`      | `$('li:even')`  | 获取到的li元素中，选择索引号为偶数的元素                     |

   3. 筛选方法

      | 语法                 | 用法                              | 描述                                                   |
      | -------------------- | --------------------------------- | ------------------------------------------------------ |
      | `parent()`           | `$('li').parent();`               | 查找父级                                               |
      | `children(selector)` | `$("ul").children('li');`         | 相当于`$('ul>li')`，最近一级（亲儿子）                 |
      | `find(selector)`     | `$('ul').find('li');`             | 相当于`$('ul li')`，后代选择器                         |
      | `siblings(selector)` | `$('.first').siblings('li');`     | 查找兄弟节点，不包括自己本身                           |
      | `nextAll([expr])`    | `$('.first').nextAll;`            | 查找当前元素之后所有的同辈元素                         |
      | `prevAll([expr])`    | `$('.first').prevAll;`            | 查找当前元素之前所有的同辈元素                         |
      | `hasClass(class)`    | `$('div').hasClass('protected');` | 检查当前的元素是否含有某个特定的类，如果有，则返回true |
      | `eq(index)`          | `$('li').eq(2);`                  | 相当于`$('li:eq(2)')`，index 从 0 开始                 |

   4. 排他思想

      ```js
      // 想要多选一的效果，排他思想：当前元素设置样式，其余的兄弟元素清除样式。
      $(this).css("color", "red");
      $(this).siblings(). css("color", "");
      ```

   5. 隐式迭代

      1. 遍历内部 DOM 元素（伪数组形式存储）的过程就叫做隐式迭代。
      2. 简单理解：给匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环，简化我们的操作，方便我们调用。

   6. 链式编程

      1. 链式编程是为了节省代码量，看起来更优雅。
      2. `$(this).css('color', 'red').sibling().css('color', ''); `

8. 操作：

   1. 样式操作

      1. 方法1: 操作 css 方法

         ```js
         // 1.参数只写属性名，则是返回属性值
         var strColor = $(this).css('color');
         
         // 2.  参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号
         $(this).css(''color'', ''red'');
         
         // 3.  参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开， 属性可以不用加引号
         $(this).css({ "color":"white","font-size":"20px"});
         ```

      2. 方法2: 设置类样式方法

         ```js
         // 1.添加类
         $("div").addClass("current");
         
         // 2.删除类
         $("div").removeClass("current");
         
         // 3.切换类
         $("div").toggleClass("current");
         ```

         注意：

         1. 设置类样式方法比较适合样式多时操作，可以弥补css()的不足。
         2. 原生 JS 中 className 会覆盖元素原先里面的类名，jQuery 里面类操作只是对指定类进行操作，不影响原先的类名。

   2. 属性操作
      - 元素固有属性值：prop()
        - prop('属性')
        - prop('属性', '属性值')
     - 注意：prop() 除了普通属性操作，更适合操作表单属性：disabled / checked / selected 等。
      - 元素自定义属性值：attr()
        - attr('属性')
        - attr('属性', '属性值')
        - 注意：attr() 除了普通属性操作，更适合操作自定义属性。（该方法也可以获取 H5 自定义属性）
      - 数据缓存：data()
        - data('name')
        - data('name', 'value')
        - 注意：同时，还可以读取 HTML5 自定义属性  data-index ，得到的是数字型。
      
   3. 文本操作

      - `$('#i1').html()`		// 获取html内容
      - `$('#i1').html('<span>123<span>')`	// 设置html内容
      - `text()`、`val()`

   4. 元素操作

      1. each()

         1. 语法1：

            ```js
            $('div').each(function (index, domElement) {});
            ```

            1. each() 方法遍历匹配每一个元素，主要用于 DOM 操作，each 每一个
            2. 里面的回调函数有两个参数，index 是每个元素的索引号，domElement 是每个 DOM 元素对象，不是 jQuery 对象
            3. 所以想要使用 jQuery 方法，需要将这个 dom 对象转化为 jQuery 对象
            4. 注意：此方法用于遍历 jQuery 对象中的每一项，回调函数中元素为 DOM 对象，想要使用 jQuery 方法需要转换。

         2. 语法2：

            ```js
            $.each(object, function (index, element) {});
            ```

            1. $.each() 方法可用于遍历任何对象，主要用于处理数据，比如数组，对象
            2. 里面的函数有两个参数：index 是每个元素的索引号，element 是遍历内容
            3. 注意：此方法用于遍历 jQuery 对象中的每一项，回调函数中元素为 DOM 对象，想要使用 jQuery 方法需要转换。

      2. 创建、添加、删除

         1. 创建

            ```js
            $('<li></li>');
            ```

            动态创建了一个 `<li>` 标签

         2. 内部添加

            ```js
            element.append('内容');
            ```

            把内容放入匹配元素最后面，类似原生 appendChild。

            ```js
            element.prepend('内容')
            ```

            把内容放入匹配元素内部最前面

         3. 外部添加

            ```js
            element.after('内容');
            ```

            把内容放到元素目标后面

            ```js
            element.before('内容');
            ```

            把内容放到目标元素前面

            1. 内部添加元素，生成之后，他们是父子关系
            2. 外部添加元素，生成之后，他们是兄弟关系

         4. 删除元素

            ```js
            element.remove();	// 删除匹配的元素（本身）
            element.empty();	// 删除匹配的元素集合中的所有的子节点
            element.html('');	// 清空匹配的元素的内容
            ```

            1. remove() 删除元素本身
            2. empty() 和 html('') 作用等价，都可以删除元素里面的内容，只不过 html() 还可以设置内容。
            3. 注意：以上只是元素的创建、添加、删除方法的常用方法，其他方法请参详API。

9. jQuery 效果

   1. jQuery 给我们封装了很多动画效果，最为常见的如下：

      1. 显示隐藏：show() / hide() / toggle() ;
      2. 划入画出：slideDown() / slideUp() / slideToggle() ; 
      3. 淡入淡出：fadeIn() / fadeOut() / fadeToggle() / fadeTo() ; 
      4. 自定义动画：animate() ;

   2. 注意：

      1. 动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。
      2. jQuery为我们提供另一个方法，可以停止动画排队：stop() ;

   3. 显示隐藏

      1. `show([speed,[easing],[fn]])` ：**显示**

         显示隐藏的匹配元素

         **speed**:三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)

         **easing**:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

         **fn:**在动画完成时执行的函数，每个元素执行一次。

      2. `hide([speed,[easing],[fn]])` ：**隐藏**

         隐藏显示的元素

         **speed**:三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)

         **easing**:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

         **fn:**在动画完成时执行的函数，每个元素执行一次。

      3. `toggle([speed],[easing],[fn])` ：**显示隐藏切换**

         用于绑定两个或多个事件处理器函数，以响应被选元素的轮流的 click 事件。如果元素是可见的，切换为隐藏的；如果元素是隐藏的，切换为可见的。

         speed: 隐藏/显示 效果的速度。默认是 "0"毫秒。可能的值：slow，normal，fast。"

         easing:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

         fn:在动画完成时执行的函数，每个元素执行一次。

   4. 滑入滑出

      1. `slideDown([speed],[easing],[fn])` ：**滑出**

         通过高度变化（向下增大）来动态地显示所有匹配的元素，在显示完成后可选地触发一个回调函数。

         **speed**:三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)

         **easing**:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

         **fn**:在动画完成时执行的函数，每个元素执行一次。

      2. `slideUp([speed,[easing],[fn]])` ：**滑入**

         通过高度变化（向上减小）来动态地隐藏所有匹配的元素，在隐藏完成后可选地触发一个回调函数。

         **speed**:三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)

         **easing**:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

         **fn**:在动画完成时执行的函数，每个元素执行一次。

      3. `slideToggle([speed],[easing],[fn])` ：**滑入滑出切换**

         通过高度变化来切换所有匹配元素的可见性，并在切换完成后可选地触发一个回调函数。

         **speed**:三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)

         **easing**:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

         **fn**:在动画完成时执行的函数，每个元素执行一次。

   5. 淡入淡出

      1. `fadeIn([speed],[easing],[fn])` ：**淡入**

      2. `fadeOut([speed],[easing],[fn])` ：**淡出**

      3. `fadeTo([[speed],opacity,[easing],[fn]])` ：**修改透明度**

         把所有匹配元素的不透明度以渐进方式调整到指定的不透明度，并在动画完成后可选地触发一个回调函数。

         **speed**:三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)

         **opacity**:一个0至1之间表示透明度的数字。

         **easing**:(Optional) 用来指定切换效果，默认是"swing"，可用参数"linear"

         **fn**:在动画完成时执行的函数，每个元素执行一次。

      4. `fadeToggle([speed,[easing],[fn]])` ：**淡入淡出切换**

   6. 自定义动画

      `animate(params,[speed],[easing],[fn])`

      1. 概述

         用于创建自定义动画的函数。

         这个函数的关键在于指定动画形式及结果样式属性对象。这个对象中每个属性都表示一个可以变化的样式属性（如“height”、“top”或“opacity”）。注意：所有指定的属性必须用骆驼形式，比如用marginLeft代替margin-left.

         而每个属性的值表示这个样式属性到多少时动画结束。如果是一个数值，样式属性就会从当前的值渐变到指定的值。如果使用的是“hide”、“show”或“toggle”这样的字符串值，则会为该属性调用默认的动画形式。

      2. 参数

         **params**:一组包含作为动画属性和终值的样式属性和及其值的集合

         **speed**:三种预定速度之一的字符串("slow","normal", or "fast")或表示动画时长的毫秒数值(如：1000)

         **easing**:要使用的擦除效果的名称(需要插件支持).默认jQuery提供"linear" 和 "swing".

         **fn**:在动画完成时执行的函数，每个元素执行一次。

         **options**:动画的额外选项。如：speed - 设置动画的速度,easing - 规定要使用的 easing 函数,callback - 规定动画完成之后要执行的函数,step - 规定动画的每一步完成之后要执行的函数,queue - 布尔值。指示是否在效果队列中放置动画。如果为 false，则动画将立即开始,specialEasing - 来自 *styles* 参数的一个或多个 CSS 属性的映射，以及它们的对应 easing 函数

   7. 停止动画排队

      1. 动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。
      2. 停止动画排队的方法为：stop() ; 
      3. stop() 方法用于停止动画或效果。
      4. stop() 写到动画或者效果的前面， 相当于停止结束上一次的动画。
      5.  总结: 每次使用动画之前，先调用 stop() ,在调用动画。

   8. 事件切换

      1. jQuery中为我们添加了一个新事件 hover() ; 功能类似 css 中的伪类 :hover 。介绍如下

      2. 语法：

         ```js
         hover([over,]out)     // 其中over和out为两个函数
         ```

      3. over:鼠标移到元素上要触发的函数（相当于mouseenter）

      4. out:鼠标移出元素要触发的函数（相当于mouseleave）

      5. 如果只写一个函数，则鼠标经过和离开都会触发它

10. 事件：

    1. 事件注册

       1. jQuery 为我们提供了方便的事件注册机制，是开发人员抑郁操作优缺点如下：
       2. 优点: 操作简单，且不用担心事件覆盖等问题。
       3. 缺点: 普通的事件注册不能做事件委托，且无法实现事件解绑，需要借助其他方法。

    2. 事件处理

       1. 事件处理 on() 绑定事件

          1. 因为普通注册事件方法的不足，jQuery又创建了多个新的事件绑定方法bind() / live() / delegate() / on()等，其中最好用的是: on()

          2. on() 方法优势1：

             1. 可以绑定多个事件，多个事件处理程序

                ```js
                $('div').on({
                    click: function () {},
                    mouseenter: function () {},
                    mouseleave: function () {},
                });
                ```

                如果事件处理程序相同

                ```js
                $('div').on("mouseenter mouseleave", function(){});
                ```

          3. on() 方法优势2：

             1. 可以委派事件操作。事件委派定义是：**把原本加给子元素身上的事件绑定在父元素身上，就是把事件委派给父元素。**

                ```js
                $('ul').on('click', 'li', function(){});
                ```

                在此之前有bind()，live()，delegate() 等方法来处理事件绑定或者事件委托，最新版本的使用 on() 来代替他们

          4. on() 方法优势3

             1. on可以给未来动态创建的元素绑定事件

                ```js
                $("ol").on("click", "li", function() {
                    alert(11);
                })
                var li = $("<li>我是后来创建的</li>");
                $("ol").append(li);
                ```

       2. 事件处理 off() 解绑事件

          1. 当某个事件上面的逻辑，在特定需求下不需要的时候，可以把该事件上的逻辑移除，这个过程我们称为事件解绑。jQuery 为我们提供 了多种事件解绑方法：die() / undelegate() / off() 等，甚至还有只触发一次的事件绑定方法 one()，在这里我们重点讲解一下 off() ;

          2. 语法

             1. off() 方法可以移除通过 on() 方法添加的事件处理程序

                ```js
                $("div").off();  // 这个是解除了div身上的所有事件
                $("div").off("click"); // 这个是解除了div身上的点击事件
                $("ul").off("click", "li");
                ```

             2. 如果有的事件只想触发一次，可以使用 one() 来绑定事件

                ```js
                // one() 只能触发事件一次
                $("p").one("click", function() {})
                ```

       3. 事件处理 trigger() 自动触发事件

          1. 有些时候，在某些特定的条件下，我们希望某些事件能够自动触发, 比如轮播图自动播放功能跟点击右侧按钮一致。可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发。由此 jQuery 为我们提供了两个自动触发事件 trigger() 和 triggerHandler() ; 

          2. 语法：

             1. trigger()

                ```js
                element.click();		// 第一种简写方式
                element.trigger('click');// 第二种自动触发模式
                ```

             2. triggerHandler()

                ```js
                element.triggerHandler('click');// 第三种自动触发模式
                ```

             3. triggerHandler模式不会触发元素的默认行为，这是和前面两种的区别

    3. jQuery 事件对象

       1. jQuery 对DOM中的事件对象 event 进行了封装，兼容性更好，获取更方便，使用变化不大。事件被触发，就会有事件对象的产生。

          ```js
          element.on(events, [selector], function(event){});
          ```

          阻止默认行为：event.preventDefault() 或者 return false;

          阻止冒泡：event.stopPropagation()

       2. 注意：jQuery中的 event 对象使用，可以借鉴 API 和 DOM 中的 event 。

    4. jQuery 拷贝对象

       1. jQuery中分别为我们提供了两套快速获取和设置元素尺寸和位置的API，方便易用，内容如下。

       2. 语法

          ![jQuery 拷贝对象](G:\桌面文件\学习\前端学习\笔记\笔记图片\extend.png)

    5. jQuery 多库共存

       1. 实际开发中，很多项目连续开发十多年，jQuery版本不断更新，最初的 jQuery 版本无法满足需求，这时就需要保证在旧有版本正常运行的情况下，新的功能使用新的jQuery版本实现，这种情况被称为，jQuery 多库共存。

       2. 语法

          jQuery 解决办法：

          1. 把里面的 $ 符号统一改为 jQuery。比如 `jQuery('div')`
          2. jQuery 变量规定新的名称：`$.noConflict()`
          3. `var xx = jQuery.noConflict();`

   - 优化

     - 如何使用jQuery绑定

       ```javascript
       $('.item .title').click(function(){
           // this, $(this)
           var tt = $(this).next();
           if (tt.hasClass('hide')) {
               tt.removeClass('hide');
           } else {
               tt.addClass('hide');
           }
           $(this).parent().siblings().find('.body').addClass('hide');
       });
       $('.item .title').bind('click', function(){
           // this, $(this)
           var tt = $(this).next();
           if (tt.hasClass('hide')) {
               tt.removeClass('hide');
           } else {
               tt.addClass('hide');
           }
           $(this).parent().siblings().find('.body').addClass('hide');
       });
       ```

     - 当文档加载完毕之后，自动执行

       ```javascript
       $(function(){
           ...
       });
       ```

     - 延迟绑定：

       - `on(events,[selector],[data],fn)`：在选择元素上绑定一个或多个事件的事件处理函数。

       - on()方法绑定事件处理程序到当前选定的jQuery对象中的元素。在jQuery 1.7中，.on()方法 提供绑定事件处理程序所需的所有功能。帮助从旧的jQuery事件方法转换，see .bind(), .delegate(), 和 .live(). 要删除的.on()绑定的事件，请参阅.off()。要附加一个事件，只运行一次，然后删除自己， 请参阅.one()。

         ```javascript
         $(function(){
             $('ul').on('click', 'li', function(){
                 alert($(this).text());
             });
         });
         function Add(){
             $('ul').append('<li>666</li>');
         }
         ```

     - `return false;`

11.  jQuery 插件

    1. jQuery 功能比较有限，想要更复杂的特效效果，可以借助于 jQuery 插件完成。 这些插件也是依赖于jQuery来完成的，所以必须要先引入

    2. jQuery文件，因此也称为 jQuery 插件。

    3. jQuery 插件常用的网站：

       1. jQuery 插件库  http://www.jq22.com/     

       2. jQuery 之家   http://www.htmleaf.com/ 

          jQuery 插件使用步骤：

       3. 引入相关文件。（jQuery 文件 和 插件文件）    

       4. 复制相关html、css、js (调用插件)。

    4. **图片懒加载插件**

       图片的懒加载就是：当页面滑动到有图片的位置，图片才进行加载，用以提升页面打开的速度及用户体验。

       **代码演示：**

       懒加载只需引入html 和 js操作 即可，此插件不涉及css。

       1. 引入js

          ```js
          <script src="js/EasyLazyload.min.js"></script>
          <script>
             	lazyLoadInit({
             		showTime: 1100,
             		onLoadBackEnd: function(i, e) {
               		console.log("onLoadBackEnd:" + i);
             		},
             		onLoadBackStart: function(i, e) {
               		console.log("onLoadBackStart:" + i);
             		}
           	});
          </script>
          ```

       2. 引入 HTML

          ```js
          <img data-lazy-src="upload/floor-1-3.png" alt="">
          ```

    5. **全屏滚动插件**

       全屏滚动插件比较大，所以，一般大型插件都会有帮助文档，或者网站。全屏滚动插件介绍比较详细的网站为：

       http://www.dowebok.com/demo/2014/77/

       全屏滚动因为有多重形式，所以不一样的风格html和css也不一样，但是 js 变化不大。所以下面只演示js的引入，html和css引入根据自己实际

       项目需要使用哪种风格引入对应的HTML和CSS。

       ```js
       <script src="js/jquery.min.js"></script>
       <script src="js/fullpage.min.js"></script>
       <script>
         	$(function() {
         		$('#dowebok').fullpage({
           		sectionsColor: ['pink', '#4BBFC3', '#7BAABE', '#f90'],
           		navigation: true
         		});
       	});
       </script>
       ```

       注意：实际开发，一般复制文件，然后在文件中进行修改和添加功能。

    6. **bootstrap组件**

       ​	Bootstrap是 Twitter 公司设计的基于HTML、CSS、JavaScript开发的简洁、直观、强悍的前端开发框架，他依靠jQuery实现，且支持响应式布局，使得 Web 开发更加方便快捷。

       ​	**凡是在软件开发中用到了软件的复用，被复用的部分都可以称为组件，凡是在应用程序中已经预留接口的组件就是插件**。Bootstrap组件使

       用非常方便:  1.引入bootstrap相关css和js        2.去官网复制html

12. 扩展：

    - $.login
    - from表单验证
    - jQuery的扩展方法：
      - `jQuery.extend(object)`：扩展jQuery对象本身。
      - `jQuery.fn.extend(object)`：扩展 jQuery 元素集来提供新的方法（通常用来制作插件）。
    - 自定义jQuery扩展的正确方法
      - 自执行
      - 闭包
    - jQuery扩展实现基本验证
      - 支持是否允许为空
      - html自定义标签属性
      - 增加验证规则 + 错误提示

13. Ajax：即`Asynchronous Javascript And XML`（异步 JavaScript 和 XML），是指一种创建交互式、快速动态网页应用的网页开发技术，无需重新加载整个网页的情况下，能够更新部分网页的技术。（偷偷发送请求）

#### 六、操作元素

1. 操作元素的内容

   `innerText` 和 `innerHTML` 的区别

   1. `innerText` 标签不识别 HTML 标签（非标准的）；
   2. `innerHTML` 标签识别 HTML 标签（W3C标准、推荐使用）；
   3. `innerText` 从起始位置到终止位置的内容，但是会去除HTML标签，同时空格和换行也会去掉；
   4. `innerHTML` 起始位置到终止位置的全部内容，包括HTML标签，保留空格和换行。

2. 操作常见元素的属性

   1. src、href、title、alt等

3. 操作表单元素的属性

   1. type、value、disabled等

4. 操作元素样式属性

   1. element.style
   2. className

#### 七、自定义属性操作

1. **获取属性值**

   1. `element.属性`  -- 获取属性值
   2. `element.getAttribute('属性');`  --  获取属性值 
   3. 二者区别
      1. `element.属性` 是获取内置属性
      2. `element.getAttribute('属性');`  可用于获取自定义属性

2. **设置属性值**

   1. `element.属性 = 属性值`  -- 设置内置属性的属性值
   2. `element.setAttribute('属性', '属性值');`  --  设置自定义属性值

3. **移除属性值**

   1. `element.removeAttribute('属性')`
   2. 注：删除 `class` 标签直接 `element.removeAttribute('class')` 即可，不用将 class 改为 className 。

4. **自定义属性**

   自定义属性目的：是为了保存并使用数据。有些数据可以保存到页面中而不用保存到数据库中。

   自定义属性获取是通过getAttribute(‘属性’) 获取。

   但是有些自定义属性很容易引起歧义，不容易判断是元素的内置属性还是自定义属性。

   1. 设置自定义属性

      H5规定自定义属性 data-开头做为属性名并且赋值

   2. 获取 H5 自定义属性

      1. 兼容性获取：`element.getAttribute('data-xxx');`

      2. H5 新增 `element.dataset.index` 或者 `element.dataset['index']`

         1. `dataset` 是一个集合里面存放了所有以 data 开头的自定义属性

         2. 如果自定义属性里面有多个-链接的单词，我们获取的时候采取 驼峰命名法

            ```html
            <div data-list-name='aaa'></div>
            <script>
                var div = document.querySelector('div');
                console.log(div.dataset.listName);
                console.log(div.dataset['listName']);
            </script>
            ```

         3. 该方法较差，只支持 ie 11 以上。

5. **节点操作**

   1. **节点概述**

      1. 网页中的所有内容都是节点（标签、属性、文本、注释等），在DOM 中，节点使用 node 来表示。
      2. HTML DOM 树中的所有节点均可通过 JavaScript 进行访问，所有 HTML 元素（节点）均可被修改，也可以创建或删除。
      3. 一般地，节点至少拥有nodeType（节点类型）、nodeName（节点名称）和nodeValue（节点值）这三个基本属性。
         1. 元素节点的 nodeType 为 1
         2. 属性节点的 nodeType 为 2
         3. 文本节点的 nodeType 为 3 （文本节点包括文字、空格、换行等等）

   2. **获取元素常用的两种方式**

      1. 利用 DOM 提供的方法获取元素
         1. `document.getElemenetById();`
         2. `document.getElementsByTagName();`
         3. `document.querySelector();` 等等
         4. 逻辑性不强且繁琐
      2. 利用节点层级关系获取元素
         1. 利用父子节点关系获取元素
         2. 逻辑性强但兼容性差

   3. **父节点**

      1. 语法：`node.parentNode;`
      2. parentNode 属性可返回某节点的父节点，注意是**最近的一个父节点**
      3. 如果指定的节点没有父节点则返回 null

   4. **子节点**

      1. **所有子节点**

         1. `parentNode.childNodes` （标准）

         2. `parentNode.childNodes` 返回包含指定节点的子节点集合，该集合为即时更新集合

         3. 注意：返回值里面包含了所有的子节点，其中包括元素节点、文本节点等等

         4. 如果想要获取里面的元素节点，则需要专门的处理，所以**一般情况下并不使用 childNodes**

         5. 下面是利用 childNodes 获取元素节点办法

            ```js
            var ul = document.querySelector('ul');
            for (var i = 0; i < ul.childNodes.length; i++){
                if (ul.childNodes[i].nodeType == 1){
                    console.log(ul.childNodes[i]);
                }
            }
            ```

      2. **子元素节点**

         1. `parentNode.children` （非标准）
         2. `parentNode.children` 是一个只读属性，返回所有的子元素节点，它只返回子元素节点，其他节点不返回。
         3. 虽然 `parentNode.chlidren` 是一个非标准的，但是在各个浏览的都是支持的，所以日常使用的是这个。

      3. **其他**

         1. 获取第一个子节点
            1. `parentNode.firstChild`
            2. `firstChild` 返回的是第一个子节点（不管是文本节点还是元素节点），找不到则返回 null 
         2. 获取最后一个节点
            1. `parentNode.lastChild`
            2. `lastChild` 返回最后一个子节点（不管是文本节点还是元素节点），找不到则返回 null 
         3. 获取第一个子元素节点
            1. `parentNode.firstElementChild` 
            2. `firstElemenChild` 返回第一个子元素节点，找不到返回 null
         4. 获取最后一个子元素节点
            1. `parentNode.lastElementChild`
            2. `lastElementChild` 返回最后一个子元素节点，找不到返回 null
         5. 其中 3 和 4 两个方法有兼容性问题， IE 9 以上有兼容性问题
         6. 实际开发中的写法
            1. 第一个子元素节点：`parentNode.children[0]`
            2. 最后一个子元素节点：`parentNode.children[parentNoden.children.length - 1]`

   5. **兄弟节点**

      1. 下一个兄弟节点

         1. `node.nextSibling;`

      2. 上一个兄弟节点

         1. `node.previousSbling;`

      3. 下一个兄弟元素节点

         1. `node.nextElementSibling;`

      4. 上一个兄弟元素节点

         1. `node.previousElementSibling;`

      5. 其中 3 和 4 有兼容性问题，解决办法如下：

         ```js
         function getNextElementSibling(element) {
             var el = element;
             while (el = el.nextSibling) {
                 if (el.nodeType === 1) {
                     return el;
                 }
             }
             return null;
         } 
         ```

   6. **创建节点**

      1. `document.crentElement('tagName');`
      2. `document.crentElement('tagName');` 方法创建由 tagName 指定的 HTML 元素，因为这些元素原先不存在，是根据我们的需求动态生成的，所以称为**动态创建元素节点**

   7. **添加节点**

      1. `node.appendChild(child)`
         1. appendChild(child) 方法将一个节点添加到指定父节点列表末尾，类似于 CSS 中的 after 伪元素。
      2. `node.insertBefore(child, 指定元素)`
         1. insertBefore() 方法将一个节点添加到父节点的的子节点前面。类似于 CSS 中的 before 伪元素。

   8. **删除节点**

      1. `node.removeChild(child)`

      2. node.removeChild() 方法从 node节点中删除一个子节点，返回删除的节点。

         ```js
         <button>删除</button>
         <ul>
             <li>熊大</li>
         <li>熊二</li>
         <li>光头强</li>
         </ul>
         <script>
             // 1.获取元素
             var ul = document.querySelector('ul');
             var btn = document.querySelector('button');
             // 2. 删除元素  node.removeChild(child)
             // ul.removeChild(ul.children[0]);
             // 3. 点击按钮依次删除里面的孩子
             btn.onclick = function() {
                 if (ul.children.length == 0) {
                     this.disabled = true;
                 } else {
                     ul.removeChild(ul.children[0]);
                 }
             }
         </script>
         ```

   9. **复制节点（克隆节点）**

      1. `node.cloneNode();` 方法返回调用该方法的节点的一个副本。也称为克隆节点/拷贝节点
      2. `node.cloneNode();` 括号为空或者里面是false 浅拷贝 只复制标签不复制里面的内容
      3. `node.cloneNode(true);` 括号为true 深拷贝 复制标签复制里面的内容

6. **三种动态创建元素的区别**

   1. **三种方式：**

      - `document.write()`
      - `element.innerHTML`
      - `document.createElement()`

   2. **区别**

      1. `document.write` 是直接将内容写入页面的内容流，**但文档流执行完毕，则它会导致页面重绘**
      2. `element.innerHTML` 是将内容写入某个DOM节点中，**不会导致重绘**
      3. `innerHTML` 创建多个元素效率更高（不要拼接字符串，采用数组的形式拼接），结构稍微复杂
      4. `createElement()` 创建多个元素效率低一点，但是结构更加清晰。

   3. **效率对比**

      1. **innerHTML字符串拼接方式（效率低）**

         ```js
         <script>
             function fn() {
                 var d1 = +new Date();
                 var str = '';
                 for (var i = 0; i < 1000; i++) {
                     document.body.innerHTML += '<div style="width:100px; height:2px; border:1px solid blue;"></div>';
                 }
                 var d2 = +new Date();
                 console.log(d2 - d1);
             }
             fn();
         // 3000 毫秒左右
         </script>
         ```

      2. **createElement方式（效率一般）**

         ```js
         <script>
             function fn() {
                 var d1 = +new Date();
         
                 for (var i = 0; i < 1000; i++) {
                     var div = document.createElement('div');
                     div.style.width = '100px';
                     div.style.height = '2px';
                     div.style.border = '1px solid red';
                     document.body.appendChild(div);
                 }
                 var d2 = +new Date();
                 console.log(d2 - d1);
             }
             fn();
         // 20毫秒左右
         </script>
         ```

      3. **innerHTML数组方式（效率高）**

         ```js
         <script>
             function fn() {
                 var d1 = +new Date();
                 var array = [];
                 for (var i = 0; i < 1000; i++) {
                     array.push('<div style="width:100px; height:2px; border:1px solid blue;"></div>');
                 }
                 document.body.innerHTML = array.join('');
                 var d2 = +new Date();
                 console.log(d2 - d1);
             }
             fn();
         // 6毫秒左右
         </script>
         ```

#### 八、DOM 的核心总结

1. **创建**

   1. `documet.write()`
   2. `element.innerHTML`
   3. `document.createElement()`

2. **增加**

   1. `appendChild()`
   2. `insertBefore()`

3. **删除**

   1. `removeChild()`

4. **改**

   1. 修改元素属性：`src`、`href`、`title` 等等
   2. 修改普通元素：`innerHTML`、`innerText`
   3. 修改表单元素：`value`、`type`、`disable` 等等
   4. 修改元素样式：`style`、`className`

5. **查**

   主要获取查询dom的元素

   1. DOM 提供的API方法：`getElementById`、`getElementTagName` 古老的用法
   2. H5 新提供的方法：`querySelector`、`querySelectorAll` 提倡
   3. 利用节点操作元素：父（`parentNode`）、子（`children`）、兄（`previonsElementSibling`、`nextElementSibling`） 提倡

6. **属性操作**

   主要针对自定义属性

   1. `setAttribute`：设置dom的属性值
   2. `getAttribute`：得到dom的属性值
   3. `removeAttribute`：移除属性

#### 九、事件高级

1. **注册事件**

   1. **传统注册方式**
      1. 利用 on 开头的 onclick
      2. `<button onclick="xxx"></button>`
      3. `btn.onclick = function(){}`
      4. 特点：注册的事件的**唯一性**
      5. 同一个元素同一个事件只能设置一个处理函数，最后注册的处理函数将会覆盖前面的处理函数
   2. **监听注册方式**
      1. W3C标准 推荐方式
      2. `addEventListener()` 它是一个方法
      3. IE 9 之前的 IE 不支持此方法，可以使用 `attachEvent()` 代替
      4. 特点：同一个元素同一个事件可以注册多个监听器
      5. 按注册顺序依次执行

2. **事件监听**

   1. `eventTarget.addEventListener()`

      1. `eventTarget.addEventListener()` 方法将指定的监听器注册到 eventTarget（目标对象）上，当该对象触发指定的事件时，就会执行事件处理函数。
      2. 里面的事件类型是字符串，必定加引号，而且不带on；
      3. 同一个元素，同一个事件可以添加多个侦听器（事件处理程序）。

   2. `eventTarget.attachEvent()` 

      1. `eventTarget.attachEvent()` 方法将指定的监听器注册到 eventTarget（目标对象） 上，当该对象触发指定的事件时，指定的回调函数就会被执行。
      2. 不常用

   3. **事件监听兼容性解决方案**

      1. 封装一个函数，函数中判断浏览器的类型

      ```js
      function addEventListener(element, eventName, fn) {
          // 判断当前浏览器是否支持 addEventListener 方法
          if (element.addEventListener) {
              element.addEventListener(eventName, fn);
          } else if (element.attachEvent) {
              element.attachEvent('on' + eventName, fn);
          } else {
              // 相当于 element.onclick = fn;
              element['on' + eventName] = fn;
          }
      }
      ```

3. **删除事件**

   1. 传统方式
      1. `eventTarget.onclick = null;`
   2. 方法监听注册方式
      1. `eventTarget.removeEventListener(type, listener[, useCapture]);`

4. **DOM事件流**

   1. html中的标签都是相互嵌套的，我们可以将元素想象成一个盒子装一个盒子，document是最外面的大盒子。

   2. 当你单击一个div时，同时你也单击了div的父元素，甚至整个页面。

   3. 事件流描述的是从页面中接收事件的顺序。

   4. 事件发生时会在元素节点之间按照特定的顺序传播,这个传播过程即DoM事件流。

   5. 我们给页面中的一个div注册了单击事件，当你单击了div时，也就单击了body，单击了html，单击了document。

   6. **DOM 事件流 分为三个阶段**

      1. 捕获阶段

         ```js
         <div class="father">
             <div class="son">son盒子</div>
         </div>
         <script>
         	// 如果addEventListener() 第三个参数是 true 那么在捕获阶段触发
         	// document -> html -> body -> father -> son
         	var son = document.querySelector('.son');
             // 给son注册单击事件，第3个参数为true
             son.addEventListener('click', function() {
                 alert('son');
             }, true);
             var father = document.querySelector('.father');
             // 给father注册单击事件，第3个参数为true
             father.addEventListener('click', function() {
                 alert('father');
             }, true);
             // 给document注册单击事件，第3个参数为true
             document.addEventListener('click', function() {
                 alert('document');
             }, true)
         </script>
         ```

      2. 当前目标阶段

      3. 冒泡阶段

         ```js
         <div class="father">
             <div class="son">son盒子</div>
         </div>
         <script>
             // onclick 和 attachEvent（ie） 在冒泡阶段触发
             // 冒泡阶段 如果addEventListener 第三个参数是 false 或者 省略 
             // son -> father ->body -> html -> document
             var son = document.querySelector('.son');
             // 给son注册单击事件
             son.addEventListener('click', function () {
                 alert('son');
             }, false);
             // 给father注册单击事件
             var father = document.querySelector('.father');
             father.addEventListener('click', function () {
                 alert('father');
             }, false);
             // 给document注册单击事件，省略第3个参数
             document.addEventListener('click', function () {
                 alert('document');
             })
         </script>
         ```

   7. 注意

      1. JS 代码只能执行捕获或者冒泡其中的一个阶段
      2. onclick 和 attacheEvent 只能到冒泡阶段
      3. `eventTarget.removeEventListener(type, listener[, useCapture]);`第三个参数如果是true，表示在事件捕获阶段调用事件处理程序；如果是false (不写默认就是false)，表示在事件冒泡阶段调用事件处理程序。
      4. 实际开发中我们很少使用事件捕，我们更关注事件冒泡。
      5. 有些事件是没有冒泡的,比如onblur, onfocus, onmouseenter, onmouseleave
      6. 事件冒泡有时候会带来麻烦，有时候又会帮助很巧妙的做某些事件。

5. **事件对象**

   1. 概述

      1. 事件发生后，跟事件相关的一系列信息数据的集合都放到这个对象里面，这个对象就是事件对象。
      2. 比如：
         1. 谁绑定了这个事件。
         2. 鼠标触发事件的话，会得到鼠标的相关信息，如鼠标位置。
         3. 键盘触发事件的话，会得到键盘的相关信息，如按了哪个键。

   2. 使用

      1. 事件触发发生时就会产生事件对象，并且系统会以实参的形式传给事件处理函数。

      2. 所以，在事件处理函数中声明1个形参用来接收事件对象。

         ```js
         div.onclick = function(e) {
             e = e || window.event;
         	console.log(e);
         }
         div.addEventListener('click', function(e) {
         	console.log(e);
         });
         function(event) {
         	console.log(event);
         }
         ```

      3. event 就是一个事件对象 写到我们侦听函数的 小括号里面 当形参来看

      4. 事件对象只有有了事件才会存在，它是系统给我们自动创建的，不需要我们传递参数

      5. 事件对象 是 我们事件的一系列相关数据的集合 跟事件相关的 比如鼠标点击里面就包含了鼠标的相关信息，鼠标坐标啊，如果是键盘事件里面就包含的键盘事件的信息 比如 判断用户按下了那个键

      6. 这个事件对象我们可以自己命名 比如 event 、 evt、 e

      7. 事件对象也有兼容性问题 ie678 通过 window.event 兼容性的写法 e = e || window.event;

   3. 事件对象的属性和方法

      ![1551169931778](笔记图片\1551169931778.png)

   4. **e.target 和 this 的区别**

      1. this 是事件绑定的元素（绑定这个事件处理函数的元素） 。

      2. e.target 是事件触发的元素。

         1. 正常情况下terget 和 this是一致的，但有一种情况不同，那就是在事件冒泡时（父子元素有相同事件，单击子元素，父元素的事件处理函数也会被触发执行），这时候this指向的是父元素，因为它是绑定事件的元素对象，而target指向的是子元素，因为他是触发事件的那个具体元素对象。

         ```js
         <ul>
             <li>abc</li>
             <li>abc</li>
             <li>abc</li>
         </ul>
         <script>
             var ul = document.querySelector('ul');
         	ul.addEventListener('click', function(e) {
                 // 我们给ul 绑定了事件  那么this 就指向ul  
                 console.log(this); // ul
                 // e.target 触发了事件的对象 我们点击的是li e.target 指向的就是li
                 console.log(e.target); // li
         	});
         </script>
         ```

   5. **阻止冒泡事件**

      1. 事件冒泡本身的特性，会带来坏处也会带来好处
      2. 标准写法
         1. `e.stopPropagation();`
      3. 非标准写法
         1. `e.cancelBubble = true;`

6. **事件委托**

   1. 概述
      1. 事件委托也称为事件代理，在 jQuery 里面称为事件委派。
      2. 说白了就是，不给子元素注册事件，给父元素注册事件，把处理代码在父元素的事件中执行。
   2. 原理
      1. 给父元素注册事件，利用事件冒泡，当子元素的事件触发，会冒泡到父元素，然后去控制相应的子元素。
   3. 作用
      1. 我们只操作了一次 DOM ，提高了程序的性能。
      2. 动态新创建的子元素，也拥有事件。

7. **常用鼠标事件**

   1. 属性和值

      ![1551172699854](笔记图片/1551172699854.png)

   2. 禁止选中文字和菜单

      ```js
      // 禁止右键菜单
      document.addEventListener('contextmenu', function (e) {
          e.preventDefault();
      });
      // 禁止选中文字
      document.addEventListener('selectstart', function (e) {
          e.preventDefault();
      });
      ```

   3. 鼠标事件对象

      1. 属性和值

         ![1551173103741](笔记图片/1551173103741.png)

      2. 获取鼠标坐标

         ```js
         // 鼠标事件对象 MouseEvent
         document.addEventListener('click', function (e) {
             // client 返回的是可视区域窗口的x和y的坐标
             console.log(e.clientX, e.clientY);
             // page 返回的是鼠标在文档中的x和y的坐标
             console.log(e.pageX, e.pageY);
             // screen 返回的是鼠标在电脑屏幕中的x和y的坐标
             console.log(e.screenX, e.screenY);
         });
         ```

8. **键盘事件**

   1. 键盘事件

      ```js
      // keyup 按键弹起的时候触发
      document.addEventListener('keyup', function (e) {
          console.log('keyup', e.key);
      });
      // keydown 按键按下的时候触发
      document.addEventListener('keydown', function (e) {
          console.log('keydown', e.key);
      });
      // keyPress 按键按下的时候触发 不能识别功能键，如： ctrl 和 shift
      document.addEventListener('keypress', function (e) {
          console.log('keypress', e.key);
      });
      ```

   2. 键盘事件对象

      1. keyCode：返回该键的 ASCII 值

      2. 注意

         1. onkeydown 和 onkeyup 不区分大小写， onkeypress 区分大小写
         2. 在实际开发中，更多使用 keydown 和 keyup
         3. keypress 不能识别功能键，但是 keyCode 属性能区分大小写，返回不同的 ASCII 值

         ```js
         <div class="search">
             <div class="con">123</div>
             <input type="text" placeholder="请输入您的快递单号" class="jd">
         </div>
         <script>
             // 获取要操作的元素
             var con = document.querySelector('.con');
             var jd_input = document.querySelector('.jd');
             // 给输入框注册keyup事件
             jd_input.addEventListener('keyup', function () {
                 // 判断输入框内容是否为空
                 if (this.value == '') {
                     // 为空，隐藏放大提示盒子
                     con.style.display = 'none';
                 } else {
                     // 不为空，显示放大提示盒子，设置盒子的内容
                     con.style.display = 'block';
                     con.innerText = this.value;
                 }
             })
             // 给输入框注册失去焦点事件，隐藏放大提示盒子
             jd_input.addEventListener('blur', function () {
                 con.style.display = 'none';
             })
             // 给输入框注册获得焦点事件
             jd_input.addEventListener('focus', function () {
                 // 判断输入框内容是否为空
                 if (this.value !== '') {
                     // 不为空则显示提示盒子
                     con.style.display = 'block';
                 }
             })
         </script>
         ```

#### 十、BOM

1. BOM概述

   1. BOM（Browser Object Model）即浏览器对象模型，它提供了独立于内容而与浏览器窗口进行交互的对象，其核心对象是 window。
   2. BOM 由一系列相关的对象构成，并且每个对象都提供了很多方法与属性。
   3. BOM 缺乏标准，JavaScript 语法的标准化组织是 ECMA，DOM 的标准化组织是 W3C，BOM 最初是Netscape 浏览器标准的一部分。
   4. BOM和DOM的区别
      1. DOM
         1. 文档对象模型
         2. DOM就是把文档当作一个对象来看待
         3. DOM的顶级对象是document
         4. DOM主要学习的是操作页面元素
         5. DOM是 W3C 的标准规范
      2. BOM
         1. 浏览器对象模型
         2. 把浏览器当做一个对象来看待
         3. BOM的顶级对象是window
         4. BOM学习的是浏览器窗口交互的一些对象
         5. BOM是浏览器开发厂商在各自的浏览器上定义的，所以兼容性较差

2. BOM的构成

   BOM 比 DOM 更大，它包含 DOM。

   ![1551319344183](笔记图片/1551319344183.png)

3. 顶级对象window

   window对象是浏览器的顶级对象，它具有双重角色。

   1. 它是JS访问浏览器窗口的一个接口
   2. 它是一个全局对象。定义在全局作用域中的变量、函数都会变成window对象的属性和方法。
   3. 在调用的时候可以省略window，前面学习的对话框都属于window对象方法,如`alert()`、 `prompt()`等。
   4. window 下的一个特殊属性 window.name

4. window对象的常见事件

   1. **页面窗口加载事件**
      1. 第一种
         1. `window.onload = function(){}` 或者 `window.addEventListener('load', function(){});`
         2. window.onload 是窗口 (页面）加载事件，**当文档内容完全加载完成**会触发该事件(包括图像、脚本文件、CSS 文件等), 就调用的处理函数。
         3. 注意：
            1. 有了window.onload就可以把JS代码写到页面元素的上方，因为onload是等页面内容全部加载完毕，再去执行处理函数。
            2. window.onload传统注册事件方式只能写一次,如果有多个，会以最后一个window.onload为准。
            3. 如果使用addEventtistener则没有限制
      2. 第二种
         1. `document.addEventListener('DOMContentLoaded', function () {})` 
         2. DOMContentLoaded 事件触发时，仅当DOM加载完成，不包括样式表，图片，flash等等。
         3. IE9以上才支持！！！
         4. 如果页面的图片很多的话, 从用户访问到onload触发可能需要较长的时间, 交互效果就不能实现，必然影响用户的体验，此时用 DOMContentLoaded 事件比较合适。
   2. **调整窗口大小**
      1. `window.onresize = function () {}` 和 `window.addEventListener('resize', function () {});`
      2. window.onresize 是调整窗口大小加载事件,  当触发时就调用的处理函数。
      3. 注意：
         1. 只要窗口大小发生像素变化，就会触发这个事件。
         2. 我们经常利用这个事件完成响应式布局。 **window.innerWidth：当前屏幕的宽度。**

5. **定时器**

   1. window 对象给我们提供了 2 个非常好用的方法-定时器。

      1. `setTimeout()`
      2. `setInterval()`

   2. `setTimeout()`

      1. 开启定时器

         1. `window.setTimeout(function(){}, [延迟的毫秒数]);`
         2. 其中的 window 可以省略
         3. 延迟的毫秒数省略默认是 0
         4. 因为定时器可能有很多，所以经常给定时器赋值一个标识符
         5. 普通函数是按照代码顺序直接调用。

         ```js
         <script>
             // 回调函数是一个匿名函数
             setTimeout(function() {
             	console.log('时间到了');
             }, 2000);
             function callback() {
                 console.log('爆炸了');
             }
             // 回调函数是一个有名函数
             var timer1 = setTimeout(callback, 3000);
             var timer2 = setTimeout(callback, 5000);
         </script>
         ```

      2. 停止定时器

         1. `window.clearTimeout(timeoutID)`
         2. `clearTimeout()` 方法取消了先前通过调用的 `setTimeout()` 建立的定时器
         3. 注意：
            1. window 可以省略
            2. 里面的参数就是定时器的标识符

   3. `setInterval()` 定时器

      1. `setInterval()` 
      2. `setInterval()` 方法重复调用一个函数，每隔这个时间，就去调用一次回调函数
      3. 注意：
         1. window可以省略
         2. 延迟的毫秒数省略默认是 0
         3. 因为定时器可能有很多，所以经常给定时器赋值一个标识符
         4. 第一次执行也是间隔毫秒数之后执行，之后每隔毫秒数就执行一次。
      4. 停止定时器
         1. `clearInterval()`

6. **this指向的问题**

   1. this的指向在函数定义的时候是确定不了的，只有函数执行的时候才能确定this到底指向谁，一般情况下this的最终指向的是那个调用它的对象。

   2. 全局作用域或者普通函数中this指向全局对象window（注意定时器里面的this指向window）

   3. 方法调用中谁调用this指向谁

   4. 构造函数中this指向构造函数的实例

      ```js
      <button>点击</button>
      <script>
          // this 指向问题 一般情况下this的最终指向的是那个调用它的对象
          // 1. 全局作用域或者普通函数中this指向全局对象window（ 注意定时器里面的this指向window）
          console.log(this);
      
          function fn() {
              console.log(this);
          }
          window.fn();
          window.setTimeout(function () {
              console.log(this);
          }, 1000);
      
          // 2. 方法调用中谁调用this指向谁
          var o = {
              sayHi: function () {
                  console.log(this); // this指向的是 o 这个对象
              }
          }
          o.sayHi();
          var btn = document.querySelector('button');
          btn.addEventListener('click', function () {
              console.log(this); // 事件处理函数中的this指向的是btn这个按钮对象
          })
          
          // 3. 构造函数中this指向构造函数的实例
          function Fun() {
              console.log(this); // this 指向的是fun 实例对象
          }
          var fun = new Fun();
      </script>
      ```

7. location 对象

   1. window对象给我们提供了一个location属性用于获取或设置窗体的URL,并且可以用于解析URL。因为这个属性返回的是一个对象,所以我们将这个属性也称为location对象

8. navigator 对象

   1. navigator 对象包含有关浏览器的信息，它有很多属性，我们最常用的是 userAgent，该属性可以返回由客户机发送服务器的 user-agent 头部的值。

      ```js
      if((navigator.userAgent.match(/(phone|pad|pod|iPhone|iPod|ios|iPad|Android|Mobile|BlackBerry|IEMobile|MQQBrowser|JUC|Fennec|wOSBrowser|BrowserNG|WebOS|Symbian|Windows Phone)/i))) {
          window.location.href = "";     //手机
       } else {
          window.location.href = "";     //电脑
       }
      ```

9. history对象

   1. window对象给我们提供了一个 history对象，与浏览器历史记录进行交互。该对象包含用户（在浏览器窗口中）访问过的URL。
   2. 可以实现前进后退功能。
   3. history对象一般在实际开发中比较少用，但是会在一些 OA 办公系统中见到。

#### 十一、JS执行机制

1. JS是单线程

   1. JavaScript语言的一大特点就是单线程，也就是说，同一个时间只能做一件事。这是因为JavaScript这门脚本语言诞生的使命所致——JavaScript是为处理页面中用户的交互，以及操作DOM而诞生的。比如我们对某个DOM元素进行添加和删除操作，不能同时进行。应该先进行添加，之后再删除。
   2. 单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。如果前一个任务耗时很长，后一个任务就不得不一直等着。
   3. 这样所导致的问题是： 如果 JS 执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉。

2. 同步和异步任务

   1. 概述

      1. 单线程导致的问题就是后面的任务等待前面任务完成，如果前面任务很耗时（比如读取网络数据），后面任务不得不一直等待！！
      2. 为了解决这个问题，利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，允许 JavaScript 脚本创建多个线程，但是子线程完全受主线程控制。于是，JS 中出现了**同步任务**和**异步任务**。

   2. 同步

      1. 前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的。比如做饭的同步做法：我们要烧水煮饭，等水开了（10分钟之后），再去切菜，炒菜。
      2. 同步任务指的是：在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；

   3. 异步

      1. 你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事情。比如做饭的异步做法，我们在烧水的同时，利用这10分钟，去切菜，炒菜。
      2. 异步任务指的是：不进入主线程、而进入”任务队列”的任务，当主线程中的任务运行完了，才会从”任务队列”取出异步任务放入主线程执行。

   4. 区别

      1. 本质区别就是这条流水线上各个流程的执行顺序不同

   5. 同步任务

      1. 同步任务都是在主线程上执行，形成一个**执行栈**

   6. 异步任务

      1. JS的异步通过回调函数实现。
      2. 一般而言，异步任务有以下三种类型
         1. 普通事件，如：click、resize 等
         2. 资源加载，如：load、error 等
         3. 定时器：包括setInterval、setTimeout 等
      3. 异步任务相关**回调函数** 添加到 **任务队列** 中（任务队列也称为消息队列）。

   7. **执行机制**

      1. 先执行栈中的**同步任务**。

      2. 异步任务（回调函数）放入任务队列中。

      3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取 **任务队列** 中的异步任务，于是被读取的异步任务结束等待状态，进入执行栈，开始执行。

      4. 事件循环

         1. 由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种执行机制被称为 **事件循环（event loop）** 。

         ![1551435335464](笔记图片/1551435335464.png)

         ![1551435398306](笔记图片/1551435398306.png)

#### 十二、元素偏移量 offset

1. **offset概述**

   offset 翻译过来就是偏移量， 我们使用 offset系列相关属性可以动态的得到该元素的位置（偏移）、大小等。

   1. 获得元素距离带有定位父元素的位置

   2. 获得元素自身的大小（宽度高度）

   3. 注意：返回的数值都不带单位

      ![offset属性](笔记图片/offset属性.png)

      ![offset图解](笔记图片/offset图解.png)

2. **offset 和 style 的区别**

   1. **offset**
      1. offset 可以得到任意样式表中的样式值
      2. offset 系列获得的数值是没有单位的
      3. offsetWidth 包含padding+border+width
      4. offsetWidth 等属性是只读属性，只能获取不能赋值
      5. **想要获取元素大小位置，用offset更合适**
   2. **style**
      1. style 只能得到行内样式表中的样式值
      2. style.width 获得的是带有单位的字符串
      3. style.width 获得不包含padding和border 的值
      4. style.width 是可读写属性，可以获取也可以赋值
      5. **想要给元素更改值，则需要用style改变**
   3. **因为平时我们都是给元素注册触摸事件，所以重点记住 targetTocuhes**

#### 十三、元素可视区 client

1. **client 概述**

   1. client 翻译过来就是客户端，我们使用 client 系列的相关属性来获取元素可视区的相关信息。通过 client 系列的相关属性可以动态的得到该元素的边框大小、元素大小等。

      ![client属性](笔记图片\client属性.png)

      ![client图解](笔记图片\client图解.png)

2. **淘宝 flexible.js 源码分析**

   1. 立即执行函数 (function(){})()  或者 (function(){}())
   2. 主要作用： 创建一个独立的作用域。里面的变量都是局部变量，避免了命名冲突问题。
   3. 下面三种情况都会刷新页面都会触发 load 事件。
      1. a标签的超链接
      2. F5或者刷新按钮（强制刷新）
      3. 前进后退按钮
   4. 但是 火狐中，有个特点，有个“往返缓存”，这个缓存中不仅保存着页面数据，还保存了DOM和JavaScript的状态；实际上是将整个页面都保存在了内存里。
   5. 所以此时后退按钮不能刷新页面。
   6. 此时可以使用 `pageshow` 事件来触发。，这个事件在页面显示时触发，无论页面是否来自缓存。在重新加载页面中，`pageshow` 会在 `load` 事件触发后触发；根据事件对象中的 `persisted` 来判断是否是缓存中的页面触发的 `pageshow` 事件
   7. **注意这个事件给window添加。**

#### 十四、元素滚动 scroll

1. **scroll概述**

   1. scroll 翻译过来就是滚动的，我们使用 scroll 系列的相关属性可以动态的得到该元素的大小、滚动距离等。

      ![scroll属性](笔记图片/scroll属性.png)

      ![scroll图解](笔记图片/scroll图解.png)

2. **页面被卷去的头部**

   1. 如果浏览器的高（或宽）度不足以显示整个页面时，会自动出现滚动条。当滚动条向下滚动时，页面上面被隐藏掉的高度，我们就称为页面被卷去的头部。滚动条在滚动时会触发 onscroll事件。
   2. 被卷去的头部就是 scrollTop

3. 页面被卷去的头部兼容性解决方案

   需要注意的是，页面被卷去的头部，有兼容性问题，因此被卷去的头部通常有如下几种写法：

   1. 声明了 DTD，使用 document.documentElement.scrollTop
   2. 未声明 DTD，使用  document.body.scrollTop
   3. 新方法 window.pageYOffset和 window.pageXOffset，IE9 开始支持

   ```js
   function getScroll() {
       return {
         left: window.pageXOffset || document.documentElement.scrollLeft || document.body.scrollLeft||0,
         top: window.pageYOffset || document.documentElement.scrollTop || document.body.scrollTop || 0
       };
    } 
   // 使用的时候  getScroll().left
   ```

#### 十五、三大系列总结

![三大系列总结](笔记图片\三大系列总结.png)

1. 他们主要用法：
   1. offset系列 经常用于获得元素位置   **offsetLeft  offsetTop**
   2. client经常用于获取元素大小  **clientWidth clientHeight**
   3. scroll 经常用于获取滚动距离 **scrollTop  scrollLeft  **
   4. **注意页面滚动的距离通过 window.pageXOffset  获得**

#### 十六、鼠标移入移出事件

1. 移入事件
   1. `mouseover`
      1. 只要鼠标指针移入事件所绑定的元素或其子元素，都会触发该事件
   2. `mouseenter`
      1. 只有鼠标指针移入事件所绑定的元素时，才会触发该事件
   3. 区别
      1. mouseover 鼠标经过自身盒子会触发，经过子盒子还会触发。
      2. mouseenter  只会经过自身盒子触发。
      3. 之所以这样，就是因为mouseenter不会冒泡
      4. 跟mouseenter搭配鼠标离开 mouseleave  同样不会冒泡
2. 移出事件
   1. `mouseout`
      1. 只要鼠标指针移出事件所绑定的元素或其子元素，都会触发该事件
   2. `mouseleave`
      1. 只有鼠标指针移出事件所绑定的元素时，才会触发该事件
   3. 区别
      1. 换句话说就是，如果一个元素**没有子元素**，那么该元素绑定`mouseout`或者`mouseleave`两种事件效果没有区别，鼠标每次移出元素时都只会触发一次事件；如果绑定了`mouseout`事件的元素**存在子元素**，那么，每次移出该元素时都会触发一次事件（包括**移出至外部**和**移出至子元素**），从子元素移出时也会触发一次事件。

#### 十七、动画封装函数

1. **动画实现原理**

   1. 核心原理：通过定时器 setInterval() 不断移动盒子位置。
   2. 实现步骤
      1. 获得盒子当前位置
      2. 让盒子在当前位置加上1个移动距离
      3. 利用定时器不断重复这个操作
      4. 加一个结束定时器的条件
      5. 注意此元素需要添加定位，才能使用element.style.left

2. 动画函数给不同元素记录不同定时器

   1. 如果多个元素都使用这个动画函数，每次都要var 声明定时器。我们可以给不同的元素使用不同的定时器（自己专门用自己的定时器）。

   2. **核心原理**：利用 JS 是一门动态语言，可以很方便的给当前对象添加属性。

      ```js
      function animate(obj, target) {
          // 当我们不断的点击按钮，这个元素的速度会越来越快，因为开启了太多的定时器
          // 解决方案就是 让我们元素只有一个定时器执行
          // 先清除以前的定时器，只保留当前的一个定时器执行
          clearInterval(obj.timer);
          obj.timer = setInterval(function() {
              if (obj.offsetLeft >= target) {
                  // 停止动画 本质是停止定时器
                  clearInterval(obj.timer);
              }
              obj.style.left = obj.offsetLeft + 1 + 'px';
      
          }, 30);
      }
      ```

3. 缓动效果原理 

   1. 缓动动画就是让元素运动速度有所变化，最常见的是让速度慢慢停下来
   2. 思路
      1. 让盒子每次移动的距离慢慢变小，速度就会慢慢落下来。
      2. 核心算法： (目标值 - 现在的位置)   /  10    做为每次移动的距离步长
      3. 停止的条件是： 让当前盒子位置等于目标位置就停止定时器  
      4. 注意步长值需要取整 

4. 动画函数添加回调函数

   1. 回调函数原理：函数可以作为一个参数。将这个函数作为参数传到另一个函数里面，当那个函数执行完之后，再执行传进去的这个函数，这个过程就叫做回调。
   2. 回调函数写的位置：定时器结束的位置。

5. 完整代码

   ```js
   function animate(obj, target, callback) {
       // 先清除以前的定时器，只保留当前的一个定时器执行
       clearInterval(obj.timer);
       obj.timer = setInterval(function() {
           // 步长值写到定时器的里面
           // 把我们步长值改为整数 不要出现小数的问题
           var step = (target - obj.offsetLeft) / 10;
           step = step > 0 ? Math.ceil(step) : Math.floor(step);
           if (obj.offsetLeft == target) {
               // 停止动画 本质是停止定时器
               clearInterval(obj.timer);
               // 回调函数写到定时器结束里面
               // if (callback) {
               //     // 调用函数
               //     callback();
               // }
               callback && callback();
           }
           // 把每次加1 这个步长值改为一个慢慢变小的值  步长公式：(目标值 - 现在的位置) / 10
           obj.style.left = obj.offsetLeft + step + 'px';
       }, 15);
   }
   ```


####  十八、触屏事件

1. **触屏事件概述**

   1. 移动端浏览器兼容性较好，我们不需要考虑以前 JS 的兼容性问题，可以放心的使用原生 JS 书写效果，但是移动端也有自己独特的地方。比如触屏事件 touch（也称触摸事件），Android和 IOS 都有。

   2. touch 对象代表一个触摸点。触摸点可能是一根手指，也可能是一根触摸笔。触屏事件可响应用户手指（或触控笔）对屏幕或者触控板操作。

   3. 触屏事件

      | 触屏 touch 事件 | 说明                            |
      | --------------- | ------------------------------- |
      | touchstart      | 手指触摸到一个 DOM 元素时触发   |
      | touchmove       | 手指在一个 DOM 元素上滑动时触发 |
      | touchend        | 手指从一个 DOM 元素上移开时触发 |

2. **触摸事件对象（TouchEvent）**

   1. TouchEvent 是一类描述手指在触摸平面（触摸屏、触摸板等）的状态变化的事件。这类事件用于描述一个或多个触点，使开发者可以检测触点的移动，触点的增加和减少，等等

   2. touchstart、touchmove、touchend 三个事件都会各自有事件对象。

   3. 三个常见对象列表：

      | 触摸列表       | 说明                                             |
      | -------------- | ------------------------------------------------ |
      | touches        | 正在触摸屏幕的所有手指的一个列表                 |
      | targetTouches  | 正在触摸当前 DOM 元素上的一个手指的一个列表      |
      | changedTouches | 手指状态发生改变的列表，从无到有，从有到无的变化 |

      - **注：因为平时我们都是给元素注册触摸事件，所以重点记住 targetTocuhes**

3. **移动端拖动元素**

   1. touchstart、touchmove、touchend可以实现拖动元素

   2. 但是拖动元素需要当前手指的坐标值 我们可以使用  targetTouches[0] 里面的pageX 和 pageY 

   3. 移动端拖动的原理：    手指移动中，计算出手指移动的距离。然后用盒子原来的位置 + 手指移动的距离

   4. 手指移动的距离：  手指滑动中的位置 减去  手指刚开始触摸的位置

      拖动元素三步曲：

      1. 触摸元素 touchstart： 获取手指初始坐标，同时获得盒子原来的位置
      2. 移动手指 touchmove： 计算手指的滑动距离，并且移动盒子
      3. 离开手指 touchend:

      - **注意： 手指移动也会触发滚动屏幕所以这里要阻止默认的屏幕滚动 e.preventDefault();**
   
4. **classList 属性**

   classList属性是HTML5新增的一个属性，返回元素的类名。但是ie10以上版本支持。该属性用于在元素中添加，移除及切换 CSS 类。有以下方法：

   **添加类**

   `element.classList.add('类名');`

   **移除类**

   `element.classList.remove('类名');`

   **切换类**

   `element.classList.toggle('类名');`

5. **click 延时解决方案**

   1. 概述

      1. 移动端 click 事件会有 300ms 的延时，原因是移动端屏幕双击会缩放(double tap to zoom) 页面。

   2. 解决方案

      1. 禁用缩放。 浏览器禁用默认的双击缩放行为并且去掉300ms 的点击延迟。

         ```html
         <meta name="viewport" content="user-scalable=no">
         ```

      2. 利用touch事件自己封装这个事件解决300ms 延迟。 

         1. 原理
            1. 当我们手指触摸屏幕，记录当前触摸时间
            2. 当我们手指离开屏幕， 用离开的时间减去触摸的时间
            3. 如果时间小于150ms，并且没有滑动过屏幕， 那么我们就定义为点击
         2. 代码

         ```js
         //封装tap，解决click 300ms 延时
         function tap (obj, callback) {
             var isMove = false;
             var startTime = 0; // 记录触摸时候的时间变量
             obj.addEventListener('touchstart', function (e) {
                 startTime = Date.now(); // 记录触摸时间
             });
             obj.addEventListener('touchmove', function (e) {
                 isMove = true;  // 看看是否有滑动，有滑动算拖拽，不算点击
             });
             obj.addEventListener('touchend', function (e) {
                 if (!isMove && (Date.now() - startTime) < 150) {  // 如果手指触摸和离开时间小于150ms 算点击
                     callback && callback(); // 执行回调函数
                 }
                 isMove = false;  //  取反 重置
                 startTime = 0;
             });
         }
         //调用  
           tap(div, function(){   // 执行代码  });
         ```

   3. 使用插件。fastclick 插件解决300ms 延迟。

      ```html
      <script src="fastclick.js"></script>
      <script>
      	if ('addEventListener' in document) {
              document.addEventListener('DOMContentLoaded', function() {
                  FastClick.attach(document.body);
              }, false);
          }
      </script>
      ```

6. 移动端常用开发框架

   1. 框架概述
      1. 框架，顾名思义就是一套架构，它会基于自身的特点向用户提供一套较为完整的解决方案。框架的控制权在框架本身，使用者要按照框架所规定的某种规范进行开发。
      2. 插件一般是为了解决某个问题而专门存在，其功能单一，并且比较小。
      3. 前端常用的框架有 Bootstrap、Vue、Angular、React 等。既能开发PC端，也能开发移动端
      4. 前端常用的移动端插件有 swiper、superslide、iscroll等。
      5. 框架： 大而全，一整套解决方案
      6. 插件： 小而专一，某个功能的解决方案
   2. Bootstrap
      1. Bootstrap 是一个简洁、直观、强悍的前端开发框架，它让 web 开发更迅速、简单。
      2. 它能开发PC端，也能开发移动端 
      3. Bootstrap JS插件使用步骤：
         1. 引入相关js 文件
         2. 复制HTML 结构
         3. 修改对应样式
         4. 修改相应JS 参数

#### 十九、本地存储

1. 本地存储特性

   1. 数据存储在用户浏览器中
   2. 设置、读取方便、甚至页面刷新不丢失数据
   3. 容量较大，sessionStorage约5M、localStorage约20M
   4. 只能存储字符串，可以将对象JSON.stringify() 编码后存储

2. window.sessionStorage

   1. 生命周期为关闭浏览器窗口

   2. 在同一个窗口(页面)下数据可以共享

   3. 以键值对的形式存储使用

   4. 存储数据：
      `sessionStorage.setItem(key, value);`

   5. 获取数据：

      `sessionStorage.getItem(key);`

   6. 删除数据：
      `sessionStorage.removeItem(key);`

   7. 清空数据：
      `sessionStorage.clear();`

3. window.localStorage

   1. 生命周期永久生效，除非手动删除，否则关闭页面也会存在
   2. 可以多窗口（页面）共享（同一浏览器可以共享）
   3. 以键值对的形式存储使用
   4. 存储数据：
      `localStorage.setItem(key, value)`
   5. 获取数据：
      `localStorage.getItem(key)`
   6. 删除数据：
      `localStorage.removeItem(key)`
   7. 清空数据：
      `localStorage.clear()`

4. 记住用户名

   1. 把数据存起来，用到本地存储

   2. 关闭页面，也可以显示用户名，所以用到localStorage

   3. 打开页面，先判断是否有这个用户名，如果有，就在表单里面显示用户名，并且勾选复选框

   4. 当复选框发生改变的时候change事件

   5. 如果勾选，就存储，否则就移除

   6. 源码：

      ```js
      
      ```

      













​	



















