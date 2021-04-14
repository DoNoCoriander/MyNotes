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

### 一些简单样式

 	1. 文字在元素中的居中
     - line-height 属性设置成和父元素的height保持一致（得显式设置px）适用于单行文字
     - 父组件display设置为table或者table-cell （inline 或者inline-block）子元素设置属性vertical-align: middle;适用于多行文字
     - 设置padding
 	2. 

