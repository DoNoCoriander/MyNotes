# CSS

### 一.flex布局

##### 1.flex的排列方式

flex-direction: row;   
![image](https://user-images.githubusercontent.com/73156828/113105795-93c44400-9234-11eb-9f7a-03ae9ba5ae02.png)

flex-direction: column;

![image](https://user-images.githubusercontent.com/73156828/113105752-873feb80-9234-11eb-99ed-e557a83a1a4e.png)

row-reverse和column-reverse都是把代码块的顺序给反转过来（就是从块最右边开始排）

##### 2.flex的四大概念

​    **容器、项目、主轴、交叉轴**

​	**容器** ： 如果在一个盒子上面，设置了display : flex 那么这个盒子就是一个容器

​	**项目** ： 容器的直接子元素

​	**主轴** ： 在容器中，项目默认是按主轴方向排列，默认是从左向右排列 X轴

​	**交叉轴** ： 与主轴垂直的轴 也就是Y轴

##### 3.容器相关的属性

###### 	3.1 flex-direction  

​		 改变主轴的方向

```css
	row // (默认值) 主轴为水平方向  从左到右
	row-reverse // 主轴方向为水平方向  起点在右端
	column // 主轴为垂直方向 起点在上沿
	Column-reverse // 主轴为垂直方向 起点在下沿
```

###### 	3.2 flex-wrap 

​		项目足够多的时候，是否需要换行

```css
	wrap // 换行 第一行在上方
	nowrap // 不换行 （默认值）
	wrap-reverse // 换行 第一行在下方
```

###### 	3.3 flex-flow 

​			是 flex-direction和flex-wrap的简写形式  默认值为 row   nowrap

###### 	3.4 justify-content

​			定义了主轴上面的对齐方式		

```css
	flex-start // 默认值 左对齐
	flex-end // 右对齐
	center // 居中	
	space-between // 两端对齐  项目之间的间隔都相等
	space-around // 每个项目的两侧的间隔都相等 所以项目之间的间隔要比两侧的要大
```
![image](https://user-images.githubusercontent.com/73156828/119305697-a9397580-bc9b-11eb-8304-1346f76ed7e2.png)

###### 3.5 align-items

​		定义项目在交叉轴上如何对齐

```css
  flex-start // 交叉轴的起点对齐
  flex-end // 交叉轴的终点对齐
  center // 交叉轴的中点对齐
  baseline // 项目的第一行文字的基线对齐
  stretch // (默认值) 如果项目未设置高度或者设为auto 将占满整个容器的高度
  space-between // 两端对齐  项目之间的间隔都相等
  space-around // 每个项目的两侧的间隔都相等 所以项目之间的间隔要比两侧的要大
```
![image](https://user-images.githubusercontent.com/73156828/119313300-f91d3a00-bca5-11eb-9b15-e76bd89b84c8.png)

###### 3.6 align-content 

​	定义各行在交叉轴上的对齐方式（将子项作为一个整体）		

##### 4.项目的相关属性

###### 	4.1 order

​		 用来改变项目的顺序

```css
    .item {
      order: <integer>;
    } // order 的值越小 此项目的位置越靠前
```

###### 	4.2 flex-grow

​			定义项目的放大比例，默认为零（即使存在剩余空间也不放大）		

```css
	.item {
      flex-grow: <number>; /* default 0 */
    }  // 如果有剩余空间的话才会生效
    // 如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。 如果一个项目的flex-grow属性为2，其他项目都为		// 1，则前者占据的剩余空间将比其他项多一倍。
```

###### 	4.3 flex-shrink

​			定义属性的缩小比例 默认为1 （如果空间不足则缩小）

```css
	.item {
      flex-shrink: <number>; /* default 1 */
    }
    // 如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。 如果一个项目的flex-shrink属性为0，其他项目都为1，     // 则空间不足时，前者不缩小。 负值对该属性无效
```

###### 	4.4 flex-basis

​			作用 ： 定义了在分配多余空间之前，项目占据的主轴空间		

```css
	.item {
		flex-basis : <length> | auto
	} 
	// 可以设置成固定值（如350px） 那样的话项目将占据固定空间
```

###### 	4.5 align-self

​		允许单个项目有与其他项目不一样的对其方式，可以覆盖align-item属性 默认值为 auto, 除了auto 其他都和align-item属性完全一致

##### 2.calc函数

可以自适应布局  动态计算位置

**注意：函数中的运算符前后需要各一个空格**

height :  calc(100% - 100px)   代表高度为其父元素的整个宽度减去100像素

##### 3.em

相对单位 参考是父元素的font-size  如果字体大小是16px那么1em就是16px

### 二.一些简单样式

##### 1.元素的垂直居中

###### 1.1 行级元素

​		1.1.1 行内包含特殊元素 ： 图片 输入框 inline-block元素

```js
		vertical-align : middle
```

​		1.1.2 设置line-height 使其和height值相等（必须要显示定义出来px）可以实现行级元素或者纯文本的块级元素的垂直居中

###### 1.2块级元素

​		1.2.1  父元素内设置display ： flex; align-items : center (兼容性比较差)

​		1.2.2  父元素设置 display ： flex; 子元素设置： align-self : center

​		1.2.3  父元素设置相对定位position: relative; 

​				   子元素设置绝对定位postion: absolute; top: 0; left:0; bottom: 0; right: 0; margin: auto;

​					关键在于设置top: 0; left:0; bottom: 0; right: 0; margin: auto表示水平、垂直4个方向的margin值都通过计算获取

​		1.2.4   利用父元素相对定位，子元素绝对定位，并且处置、水平方向个偏移50%  (子元素利用负值margin偏移自身宽度、长度的一半)

​		1.2.5  父元素添加： display: table-cell; verticle-align: middle;

​		1.2.6 使用绝对定位的translate()属性

```javascript
		父元素设置{ position: relative; }
		子元素设置{ position: absolute; top: 50%; left: 50%; transform: translate(-50%, 50%) }
```

##### 2.&符号

```javascript
.bordered {
  &.float {
    float: left; 
  }
  .top {
    margin: 5px; 
  }
等同于
 .bordered.float {
   float: left; 
 } //串联选择器  只会选择他的直接子元素
 .bordered .top {
   margin: 5px;
 }// 后代选择器  会选择他的所有子元素
```

##### 3.横线的样式

```javascript
hr{
    border: none; // 防止横线出现黑框
	height: 1px; // 横线的高度（粗细）
	background-color: #e5e5e5; //横线的颜色
}
 三种漂亮的横线样式：
 /*内嵌水平线*/
	hr {	
		width: 80%;
		margin: 0 auto;
		border: 0;
		height: 0;
		border-top: 1px solid rgba(0, 0, 0, 0.1);
		border-bottom: 1px solid rgba(255, 255, 255, 0.3);
	}
	/*透明渐变水平线*/
	hr {	
		width: 80%;
		margin: 0 auto;
		border: 0;
		height: 1px;
		background-image: linear-gradient(to right, rgba(0, 0, 0, 0), rgba(0, 0, 0, 0.75), rgba(0, 0, 0, 0));
	}
	/*渐变*/
	hr {		
		width: 80%;
		margin: 0 auto;
		border: 0;
		height: 1px;
		background: #333;
		background-image: linear-gradient(to right, #ccc, #333, #ccc);
	}
```

##### 4.滚动条

```javascript
// 元素设置高度和宽度
div {
	height : ,
	width : ,
	overflow : scroll  // 表示无论是不是需要滚动条 都会显示
			   // visible（默认值） 表示内容不会被修剪 会显示在元素的外面
			   // hidden 内容会被修剪 并且不可见
			   // auto 如果内容需要滚动条 会自动出现
			   // inherit 从父元素继承overflow的值
	overflow-x : 表示水平方向上的滚动条属性
	overflow-y : 表示垂直方向的滚动条的属性
}
```

##### 5.两个兄弟元素的叠加显示

```html
<div className = "father">
    <div className = "bro1"></div>
    <div className = "bro2"></div>
</div>
.father {
	position : 'relative'
}
.bro1 {
	position : 'absolute';
	z-index : 999(设置的大一点)
	// 添加一些其他样式 调整其的位置
}
```

##### 6.超出元素大小的文字用省略号显示

```javascript
    text-overflow: ellipsis; // 超出的部分显示省略号
    white-space: nowrap; // 不允许文字换行
    overflow: hidden; // 超出的部分隐藏
    width : //设置宽度
```

##### 7.一些简单的符号意义：~ + >

```react
// ~
p~ul选择器 p之后出现的所有ul
两种元素必须拥有相同的父元素，但是 ul不必直接紧随 p。
// >
A>B 表示选择A元素的所有子B元素
A B 表示选择所有的后代元素  A > B只能选择一代
// + 
.a + .b 相邻兄弟选择器
```

##### 8.根据顺序选择子元素

```css
div:nth-child(odd){

} // 选择奇数的子元素 div:nth-child(2n+1)
div:nth-child(even){

} // 选择偶数的子元素div:nth-child(2n)

div:nth-child(3){

} // 选择第三个子元素
div:nth-child(-n+5) {
    // 选择前五个元素
}
div:nth-child(5+n){
    // 选择第五个以后的元素
}
```





### 三.菜鸟驿站CSS笔记

#### CSS

##### 	1.CSS背景

```css
背景颜色 ： background-color 
背景图像 ： background-image : url('path') (图像默认水平和垂直平铺)
		  // 图像是否平铺
		  background-repeat: repeat-x; // 图像水平平铺		  
		                     repeat-y; // 图像垂直平铺		  
		                     repeat-x; // 图像只显示一次 不平铺
          // 图像的位置
		 background-position: x轴 y轴 （左上角是原点）
         // 背景图片是不是固定
         background-attachment: fixed; // 固定 (始终在屏幕的固定位置)
							    scroll // 随着页面的滚动而滚动
                                local // 随着元素的内容的滚动而滚动
        background : url() no-repeat pink 10px(背景图片向右移动10px)  50px(背景图片向下移动50px)
		background-size : cover // 图片以父元素的高度为准（图片的高度等于父元素的高度 图片高和宽的比不变可能不会显示完整）
						  contain // 图片以父元素的宽度为准（图片的宽度等于父元素的宽度）
```

#####      2.文本

```javascript
文本的颜色 ： { color : rgb(255, 0, 0) }
文本的对齐方式 ： {
			text-align : center // 文本居中
                         right // 右对齐
                         justify // 实现文本两边对齐
}
文本的方向： direction: rtl //文本方向从右到左。
					  ltr // 从左到右（默认）
文本字符的间距 ： letter-spacing : 2px
文本之间的行高 ： line-height : number // 设置数字，此数字会与当前的字体尺寸相乘来设置行间距。
							 length (px) // 固定的行高 
							 % // 基于当前字体尺寸的百分比行间距。
文本的添加修饰 ： text-decoration : underline // 文本下面添加一条线
								 overline // 文本上的一条线
                                 line-through // 穿过文本的一条线
								 blink // 闪烁的文字 但浏览器不会显示
               text-decoration 是 text-decoration-line
								  text-decoration-color
                                  text-decoration-style 
								的简写
文本中文本的首行缩进 ： text-indent : length // 固定的缩进
								   % // 基于父元素的宽度的百分比
文本中的阴影 ： text-shadow : 阴影的x偏移 y  模糊的大小  color
控制文本中的字母 ： text-transform : capitalize // 文本中的每个单词首字母大写
								  uppercase // 文本的变成大写字母
                                  lowercase // 变成小写字母
返回的文本被重写 ： unicode-bidi ： bidi-override // 创建附加的嵌入层面 排序取决于direction属性
                                 embed // 创建附加的嵌入层面
文本的垂直对齐 ：vertical-align :  baseline	 //默认。元素放置在父元素的基线上。
                                sub	// 垂直对齐文本的下标。
                                super ///垂直对齐文本的上标
                                top	// 把元素的顶端与行中最高元素的顶端对齐
                                text-top ///把元素的顶端与父元素字体的顶端对齐
                                middle	//把此元素放置在父元素的中部。
                                bottom	//使元素及其后代元素的底部与整行的底部对齐。
                                text-bottom	//把元素的底端与父元素字体的底端对齐。
                                length	//将元素升高或降低指定的高度，可以是负数。
                                %	//使用 "line-height" 属性的百分比值来排列此元素。允许使用负值。
                                inherit	//规定应该从父元素继承 vertical-align 属性的值。
设置元素中空白的处理方式 : white-space : nowrap // 文本不会换行 直到遇见 <br />
					   pre // 空白会被保留（文本会根据代码里面写的样子展示）
设置字间距(单词和单词之间的间距) : word-spacing :  length // 固定间距
```

##### 3.字体

```js
font :  font-style font-variant font-weight font-size/line-height font-family // font-size font-family 必需
font-family : "Times New Roman",Georgia,Serif; //字体类型
font-size : // 字体的大小
font-style(字体样式) : italic //显示一个斜体 (使用字体中的斜体)
					  oblique //  显示一个倾斜的字体 （字体中没有斜体时文字直接倾斜）
font-variant : small-caps // 小型大写字体（和小写字体一样大的大写字母）
font-weight : bold // 粗体字体
			  bolder // 更粗的字体
              lighter // 更细的字体
              100 - 700 // 由粗到细 400 -> normal   700 -> bold
```

##### 4.链接（link）（a标签）

```javascript
a:link {} // 未访问的链接
a:visited {} // 已经访问过的链接
a:hover {} // 鼠标移动到链接
a:active {} // 鼠标点击时

a:hover 必须跟在 a:link 和 a:visited后面
a:active 必须跟在 a:hover后面
// 可以使用text-decoration属性来删除链接中的下划线
```

##### 5.列表

```javascript
ul : 无序列表  ol : 有序列表
list-style-image : // 将图像设置成列表项标志
list-style-position : // 设置列表项标志的位置
					  inside outside (一个缩进多一个缩进少)
list-style-type : // 设置列表标志的类型 (实心圆 空心圆 罗马数字什么的)
```

##### 6.盒子模型

​	盒子模型 ：边距(margin)  边框(border)  填充(padding)  实际内容

​	整个元素的总宽度 ： 左边距 + 左边框  +  左填充 + 内容宽度 + 右填充 +  右边框 + 右边距

##### 7.边框

```css
//边框的样式 可以分别设置四个边的样式
border-style : none //默认值
			   dashed // 虚线边框
			   solid //实线边框
			   double // 两个边框
			   groove/ridge/inset/outset //定义的3D的边框
//边框的宽度
border-style : //需要和border-style配合使用
//边框的颜色
border-color 
// 简写形式 
border : width style color
```

##### 8.轮廓（outline）

```
outline 不占空间 属性和border相似
```

##### 9.外边距（margin）

清除元素边框外周围的元素区域  没有背景颜色 完全透明  上 右 下 左

##### 10.填充（padding）

定义边框和元素之间的空间

##### 11.分组和嵌套选择器

​	分组选择器 ： 

```css
h1, h2, p {

} // 选择了所有的h1, h2, p的标签
```

​	嵌套选择器

```css
p{ } // 为所有 p 元素指定一个样式。
.marked{ } // 为所有 class="marked" 的元素指定一个样式。
.marked p{ } // 为所有 class="marked" 元素内的 p 元素指定一个样式。
p.marked{ } // 为所有 class="marked" 的 p 元素指定一个样式
```

##### 12.尺寸（宽和高）

```css
height :  // 元素的高度
line-height : // 设置行高
			  normal // 设置合理的行间距
			  number // 此数字与当前的字体的尺寸相乘设置行间距
			  length （px） // 设置固定的行间距
			  % // 基于当前的字体的尺寸的百分比设置行间距
			  inherit // 从父元素继承
max-height : // 元素的最大高度
max-width : // 元素的最大宽度
min-height: // 元素的最小高度
min-width : // 元素的最小宽度
width : // 元素的宽度
```

##### 13.Display 和 Visibililty

```css
display : // 设置一个元素应该如何显示
		none // 元素不显示  而且不占空间
		inline // 内联元素  内联元素只需要必要的宽度，不强制换行
		block // 块级元素  一个内联元素设置为display:block是不允许有它内部的嵌套块元素
visibililty : // 设置一个元素该显示还是隐藏
		hidden // 元素不显示 但是会占空间
```

##### 14.Position

``` css
position : // 指定了元素的定位类型
		   static // 元素的默认值
		   fixed // 设置元素的位置事相对于浏览器的固定位置  即使窗口时滚动的他也不会移动
		   		 // 此元素的位置和文档流无关  因此不占据空间
		   relative // 相对位置   相对其的正常位置进行移动 （left right top bottom）
		   absolute // 绝对位置   其的位置相对于最近的已定位的父元素 若没有则相对于html 与文档流无关  不占据空间
		   // 子绝父相
		   sticky // 粘性定位 基于用户的滚动位置来定位
				  // 依赖于用户的滚动 在relative 与 fixed 定位之间切换
				  // 在跨越特定阈值前为相对定位，之后为固定定位。
				  // 这个特定阈值指的是 top, right, bottom 或 left 之一，换言之，指定 top, right, bottom 或 left 四个阈值其中之一，才可使粘性定位生效。否则其行为与相对定位相同。
```

##### 15.Overflow

```css
overflow : // 控制元素超出元素框时的显示方式
		   visible // 默认值  元素会直接显示在元素框的外面
		   hidden // 超出的部分会直接被裁减
		   scroll // 无论是否超出 浏览器都会显示滚动条
		   auto // 超出时才会出现滚动条
		   inherit // 继承父元素的此属性值
```

##### 16.Float

```css
float : // 是元素左右移动 知道其边缘碰到边缘框或者另一个浮动元素的边框
		// 浮动元素之后的元素将会围绕他
		// 对其之前的元素没有影响
		// 浮动元素不在文档流之中 所以不占空间
clear : both // 清除浮动
overflow : auto // 当子浮动元素超出父元素的大小之后设置此属性可以让子元素把父元素给撑开 
// https://zhuanlan.zhihu.com/p/142630896
```

##### 17.对齐

```css
// 元素左右居中对齐
margin : 0 auto // 水平居中块级元素（需要设置width属性）
text-align : center // 文本居中
position : absolute // 使用定位方式设置left  right  top bottom 时期与边缘对齐
float : left/right  // 使用浮动是元素左右对齐
// 元素上下居中对齐
padding : 10px 0px // 设置元素的padding使其上下padding值相等
line-height : px // 设置行高和元素的高度一致（仅对单行文本有效 对行需要设置其他样式）
```

##### 18.组合选择器

```css
后代选择器(以空格     分隔)  // 选择所有的子元素
子元素选择器(以大于 > 号分隔）// 选择其的直接子元素
相邻兄弟选择器（以加号 + 分隔）
普通兄弟选择器（以波浪号 ～ 分隔）
```

##### 19.伪类

```css
元素:伪类 {
    
}
q:lang(langName) {
    quotes : "左边符号"  "右边符号";
}
q元素
<p>我是p元素<q>我是q元素里面的</q></p>
我是p元素左边符号我是q元素里面的右边元素
```

##### 20.伪元素

```
伪类和伪元素的区别 ： 
	伪类 ： 伪类选择元素基于的是当前元素处于的状态
	伪元素 ： 伪元素是对元素中的特定内容进行操作 动态性比伪类要低
```

##### 21.图像的透明和不透明

```css
img {
    opacity // 0-1 值越小越透明
}
```

##### 22.img

```css
img 自适应父元素的大小
img {
    // 图片以父元素的宽度为准进行缩放
	width : 100%;
    height : auto;
    // 图片以父元素的高度为准进行缩放
   	width : auto;
    height : 100%;
}
```

##### 23.@media

```css
@media 查询
    @media not|only mediatype and (expressions) {
    CSS 代码...;
}
媒体类型 ： all // 所有设备
	      print // 适用于打印机
		  screen // 用于电脑屏幕 手机  平板等
		  speech // 屏幕阅读器等发声设备
```

##### 24.属性选择器

```css
选择具有特定属性的HTML元素样式
[title] {
    // 选择所有具有title属性的元素
}
[title = titleValue] {
    // 选择属性title等于titleValue的元素
}
[title~=titleValue] {
    // 选择属性之中有title的值的 例如：
    <div title = 'titleValue otherValue'></div>
}
input[type=text]{
    // 选择type值为text的input标签
}

CSS 属性选择器 ~=, |=, ^=, $=, *= 的区别

1.attribute 属性中包含 value:　
  [attribute~=value] 属性中包含独立的单词为 value，例如：
         [title~=flower]  -->  <img src="/i/eg_tulip.jpg" title="tulip flower" />
  [attribute*=value] 属性中做字符串拆分，只要能拆出来 value 这个词就行，例如：
         [title*=flower]   -->  <img src="/i/eg_tulip.jpg" title="ffffflowerrrrrr" />
2.attribute 属性以 value 开头:
  [attribute|=value] 属性中必须是完整且唯一的单词，或者以 - 分隔开：，例如：
		 [lang|=en]     -->  <p lang="en">  <p lang="en-us">
  [attribute^=value] 属性的前几个字母是 value 就可以，例如：
		 [lang^=en]    -->  <p lang="ennn">
3.attribute 属性以 value 结尾:
  [attribute$=value] 属性的后几个字母是 value 就可以，例如：
		 a[src$=".pdf"]
```

##### 25.计数器

```css
counter-reset - 创建或者重置计数器
counter-increment - 递增变量
content - 插入生成的内容
counter() 或 counters() 函数 - 将计数器的值添加到元素

body {
		counter-reset : mycounterone
	}
h2::before{
    counter-increment : mycounterone;
    content : "第"counter(mycounterone)"个  "
}
```

#### CSS3

##### 1.边框

```css
border-radius // 圆角边框
			左上 右上  右下 左下
// 盒子阴影
box-shadow : 水平阴影（必须） 垂直阴影（必须） 模糊距离 阴影的大小 阴影颜色 // 阴影
border-image :<‘border-image-source’> || <‘border-image-slice’> [ / <‘border-image-width’> | / <‘border-image-width’>? / <‘border-image-outset’> ]? || <‘border-image-repeat’>// 边界图片
	border-image-source: 图片的地址
	bordre-image-slice //边框图像切片。指定4个值(4条分割线：top, right, bottom, left)将图片分割成9宫格 值为number
	   fill 会把中间的那一部分当作此节点的背景
	border-image-width : 边框图片宽度
    border-image-outset : 边框图片开端
		// 指定边框到元素的距离
	border-image-repeat : 边框图片平铺
		// stretch 不重复会拉伸
		// repeat 重复但可能会不会完整 
		// round 重复而且完整 
		// space 重复 之间会有空隙
```

##### 2.背景

```css
// 背景图片为多张图片组合而成 在最上面的是第一张
background-image: url(img_flwr.gif), url(paper.gif); 
background-position: right bottom, left top; 
background-repeat: no-repeat, repeat; 
// background-origin  设置把背景图片的位置区域
border-box  --> padding-box ---> content-box
// background-clip // 规定背景的绘制区域
border-box  --> padding-box ---> content-box
```

##### 3.渐变

```css
// 线性渐变  默认是从上到下
background-image: linear-gradient(to right （也可以写角度）, red 30%(此颜色占的大小), green, blue);
// 重复线性渐进  不均匀渐变百分比的学习。百分比表示指定颜色的标准中心线位置，百分比之间是过渡色
background-image: repeating-linear-gradient(red, yellow 10%, green 20%);
// 径向渐变
background-image: radial-gradient(red 5%, yellow 15%, green 60%);
background-image: radial-gradient(circle(圆形渐变 默认为椭圆渐变), red, yellow, green);
// 重复的径向渐变
repeating-radial-gradient
```

##### 4.文本效果

```css
text-shadow : // 文本的阴影
	// 水平阴影，垂直阴影，模糊的距离，以及阴影的颜色
text-overflow : // 文本超出父元素的部分
	ellipsis // 超出部分用... 表示
	clip // 默认值 直接被裁剪
word-wrap : // 长文本是换行规则
	break-word : 一个单词超过元素边界就阶段单词换行（但此元素还是会先换行）
word-break ： 
	break-all : 元素本行剩下的空间不够这个单词阶段单词并换行	
```

##### 5.字体

```css
@font-face { // 用户的浏览器会自动下载字体文件
    font-family : myFontFamily;
    src:url('字体文件的存放位置');
    font-weight : bold; // 使用粗体文字时需要设置
}
p {
    font-family : myFontFamily;
}
```

##### 6.2D转换

```css
translate() //根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动。
	transform: translate(10px, 30px) //向左移动10px 向下移动30px 百分比是此元素的百分比大小
rotate() // 在一个给定度数顺时针旋转的元素。负值是允许的，这样是元素逆时针旋转。
	transform: rotate(30deg); // 以中心点为轴 顺时针旋转三十度
scale() // 该元素缩放的大小，取决于宽度（X轴）和高度（Y轴）的参数：
	transform: scale(2,3); 宽度 * 2，高低 * 3。
skew() // 
	transform:skew(30deg,20deg); //x轴上倾斜（逆时针）30 y轴顺时针倾斜20度
matrix()
	// 矩阵
```

##### 7.3D转换

```css
rotateX() // 沿着X轴旋转
	transform: rotateX(120deg) // 沿X轴旋转120度
rotateY() // 沿着Y轴旋转

transform-origin ： // 设定变换的原点
```

##### 8.过渡

```css
transition // 元素逐渐从一个样式变为另一个样式
	// 变换的属性名  过渡效果花费的时间  过渡效果的时间曲线  延时时间 	
```

##### 9.动画

```css
@keyframes // 创建动画
@keyframes 动画名字 {
    from {
        // 开始时的样式
    }
    to {
        // 最终样式
    }
}

div {
    animation ： 动画名字  动画变换时长 动画的切入方法（又快到慢什么的） 延时 次数 动画方向;
}
```

##### 10.多列

```css
// 多列  将文本分成多列
column-count : // 将文本分成的列数
column-gap : // 分成的多列之间的间隙
column-rule-style : // 指定了列与列间的边框样式
column-rule-width : // 指定了两列的边框厚度
column-rule-color : // 指定了两列的边框颜色
column-rule : 设置了列直接的边框的厚度，样式及颜色
column-span : 指定 <h2> 元素跨越所有列
column-width : 指定了列的宽度
```

##### 11.用户界面（用户调整元素尺寸 框尺寸 外边框）

```css
resize : // 指定一个元素可不可以由用户调整大小
	both // 宽度和高低都可以调整
	horizontal // 可以调整元素的宽度
	vertical // 调整元素的高度
box-sizing : // 指定元素的最终尺寸计算方式
	content-box : 元素的宽度和高度不包括padding border (默认值) 最终尺寸：width + padding * 2 + border * 2
	border-box : 最终尺寸为 width 
outline-offset : // 外形修饰 轮廓
	轮廓与border相似 但 1.轮廓不占用空间 2.轮廓可能是非矩形
```

##### 12.图片

```css
img {
    border-radius : 10px // % 圆角图片
    padding
    border
    filter :  // 给图片加滤镜
}
```

##### 13.设备宽度

```css
device-width/height  ：定义输出设备的屏幕可见宽/高度 基本与@media配合使用
```

### 四.CSS 变量

##### 1.变量的声明

​	声明变量时，变量名前面要加两根连词线（--）

```css
body {
    --name-input-color : red;
} 
// 表示在body里面声明了一个名为 --name-input-color 值为 red 的变量

:root {
    
} // 表示在根标签下声明变量
```

##### 2.var() ---> 读取变量

```css
p {
    color : var(--name-input-color, green);
    // 第二个参数表示参数的默认值  第二个参数不处理内部的逗号或空格，都视作参数的一部分
}
```

```css
// 如果变量是数值 不能和单位直接连用 必须使用calc()函数
p {
  margin-top : calc(var(--top) * 1px) 
}
```

```css
// 变量和字符串连接
p:after {
    content : 'content'var(--content);
}
```

### 五. CSS技巧

##### 1.透明边框

```css
background-color: red;
border: 20px solid rgba(0, 0, 0, 0.5);
```

​	设置边框的透明度的时候边框的颜色会被内部的背景颜色侵入而不是透出外部的背景颜色 即边框的颜色是透明度为0.5的红色

需要添加**background-clip**属性来设置背景的绘制区域

```css
background-clip: padding-box;
// 默认值是border-box
```

##### 2.多重边框

​	设置两层边框时 可以使用border + outline

```css
border: 10px solid darkgreen;
outline: 5px dashed wheat;
```

​	两层以上的边框时只能使用**box-shadow**来模拟(缺点时只能模拟实线效果)

```css
box-shadow: 0 0 0 10px greenyellow,
            0 0 0 20px green;
```

##### 3.背景定位

对背景图片的位置添加偏移量

```css
background: background: url("favicon.png") right 20px bottom 10px no-repeat greenyellow;
//  背景图片的位置距离右侧有20px 下部有10px
background-position: right calc(100% - 10px) top calc(100% - 10px)

// 背景图片的位置和内边距有关系时
background-origin: content-box; // 设置背景图片位置 默认值padding-box
```

##### 4.边框内圆角

```css
<div class = "root-div">
	<div></div>
</div>

.root-div {
    padding : 10px;
    background : red
}

.root-div {
    border-radius : 0.8em;
    background : green;
}
```

##### 5.条纹

垂直或者水平条纹

```css
background: linear-gradient(to right, red 50%, yellow 50%);
background-size : 30px 100%;
```

带角度的倾斜条纹

两种颜色就需要四个色标

```css
background: repeating-linear-gradient(45deg, red, yellow 15px, red 15px, yellow 30px);
```

