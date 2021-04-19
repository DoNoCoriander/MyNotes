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

##### 1.文字在元素中的居中

 - line-height 属性设置成和父元素的height保持一致（得显式设置px）适用于单行文字
 - 父组件display设置为table或者table-cell （inline 或者inline-block）子元素设置属性vertical-align: middle;适用于多行文字
 - 设置padding
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

