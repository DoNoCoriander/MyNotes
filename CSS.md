# CSS

### 一.flex布局

##### 1.flex的排列方式

flex-direction: row;   
![image](https://user-images.githubusercontent.com/73156828/113105795-93c44400-9234-11eb-9f7a-03ae9ba5ae02.png)

flex-direction: column;

![image](https://user-images.githubusercontent.com/73156828/113105752-873feb80-9234-11eb-99ed-e557a83a1a4e.png)

row-reverse和column-reverse都是把代码块的顺序给反转过来（就是从块最右边开始排）



##### 2.calc函数

可以自适应布局  动态计算位置

height :  calc(100% - 100px)   代表高度为其父元素的整个宽度减去100像素

3.em

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

​		1.2.1  父元素内设置display ： flex; align-item : center (兼容性比较差)

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

### 三.菜鸟驿站CSS笔记

##### 	1.CSS背景

```javascript
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

