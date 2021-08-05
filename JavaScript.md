##                                                    JavaScript

### 一.Promise

#### 1.Promise 构造器

```javascript
var promise = new Promise(function (resolve, reject) {

})
```

#### 2.Promise 的一些静态方法

- Promise.all

```javascript
  Promise.all([promise1, promise2, ...]).then(function (res) {
		
	}).catch(function (error) {
        
    })// 所有的promoise都resolve 再执行then
	  // 参数是一个数组
	  // 如果有的promise执行了reject方法 那么catch方法将会捕捉第一个error
	  // 返回的结果也会组成一个数组  顺序和参数的顺序一致
	  // 有一个reject的话 其他的promise及其结果会被忽略 
```

- Promise.race

```javascript
  Promise.race([promise1, promise2, ...]).then(function (res) {
		
	}).catch(function (error) {
        
    })// 所有的promise  只要有一个执行结束 就会触发
	  // 参数是一个数组
```

- Promise.resolve
- Promise.reject

```javascript
  Promise.resolve(value) // 可以手动控制此Promise的返回状态
  Promise.reject(error)
```

- Promise.allSettled

```javascript
	Promise.allSettled([...promise...]).then(res => {
	
	})// 等待所有的promise都结束后 以包含状态和返回值的对象数组的形式返回结果 [{status : "fulfilled", values / reason}]
```



### 二. JSON

 1. JSON.parse() 

    将一个字符串转换成JS对象

```javascript
    JSON.parse(text, fun(key, value));
        fun --> 一个转换结果的函数， 将为对象的每个成员调用此函数。
        以键值对的格式进行遍历 最后一个参数key : '' , value : 转换之后的text
```

2. JSON.stringify()

   将 JS 对象转换成字符串

   ```javascript
   JSON.stringify(value, replacer, space)
   
       value:
       必需， 要转换的 JavaScript 值（通常为对象或数组）。
   
       replacer:
       可选。用于转换结果的函数或数组。
   
       如果 replacer 为函数，则 JSON.stringify 将调用该函数，并传入每个成员的键和值。使用返回值而不是原始值。如果此函数返回 undefined，则排除成员。根对象的键是一个空字符串：""。
   
       如果 replacer 是一个数组，则仅转换该数组中具有键值的成员(可以用来指定转换对象中的那些属性)。成员的转换顺序与键在数组中的顺序一样。当 value 参数也为数组时，将忽略 replacer 数组。
   
       space:
       可选，文本添加缩进、空格和换行符，如果 space 是一个数字，则返回值文本在每个级别缩进指定数目的空格，如果 space 大于 10，则文本缩进 10 个空格。space 也可以使用非数字，如：\t。
   ```


### 三. 数据类型

#### 	基本数据类型：

​		Number 类型 ：NaN === NaN  ---->  false

​		string  字符串类型

​		布尔值 ：

​		Null

​		Undefined

​		Symbol (ES6)

​		bigint (ES10)

#### 	引用数据类型 ： 

​		Object	

```javascript
const zhao = {
    'north-west' : '西北',
};// 属性名必须是一个有效的变量名  否则必须要用’‘括起来  而且访问的时候只能使用[]的方法访问不能使用 . 访问
zhao["north-west"] -----> 西北
```

#### Map

键值对的结构 具有极快的查找速度

```javascript
var map = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]) //  let map = new Map()
map.set("暗号", "宝塔镇河妖");
map.set(1, 12); // 添加元素  返回值是map
const d = map.delete('name'); // 删除元素 d ---> true
map.get("暗号") // 获取元素 '宝塔镇河妖'

Map的一个key只能对应一个value 多次对一个key放入value 后面的会把前面的值给冲掉
```

#### Set

`Set`和`Map`类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在`Set`中，没有重复的key。

重复的元素会直接被过滤

```javascript
var set = new Set() // 创建空Set
var set = new Set([1, 4, 'string']) // 有初始值的set
set.add(key) // 添加元素
set.delete(key) // 删除元素
```

### 四.原型和原型链 继承



#### 原型继承  

```javascript
function Person () {
    
}

function Student () {
    
}

1. 最简单的继承方法
	Student.prototype = Person.prototype
	缺点：子类和父类的原型指向了同一个对象 子类的prototype修改的时候也会影响到父类的原型
2. 通过一个中间类来解决上面的问题
	function Middle () {}
	
	Middle.prototype = Person.prototype
	Student.prototype = new Middle()
	Student.prototype.constructor = Student;
```



### 五. 正则表达式

```javascript
\d  匹配数字
\D	匹配非数字字符
\w  匹配一个字母、数字和下划线 等价于'[A-Za-z0-9_]'
\W 	匹配非字母数字下划线  等价于'[^A-Za-z0-9_]'
\s	匹配所有空白符
\S	匹配所有非空白符
.   匹配任意字符（除换行符（\n、\r））
* 	表示任意个字符 \d* ----> 任意个数字
?	匹配0或1个字符
+ 	表示至少一个字符
{n}	表示n个字符
{n,} 表示至少匹配n次
{n, m}  表示 n 到 m 个字符
[字符]	匹配[]中间的所有字符 [A-Z] ----> 表示匹配A到Z的所有字母
[^字符]	匹配[]中间以外的所有字符
$	匹配每行字符串的结尾位置
^ 	匹配每行字符串的开始位置
\b 匹配一个单词边界（字与空格间的位置）
\B 匹配非单词边界（会匹配单词中间字母和字母之间的位置）
贪婪和非贪婪：
	// <h1>正则表达式</h1>
	/<.*>/  ------> 贪婪模式 ： ——————> 会匹配整个<h1>正则表达式</h1>
 	/<.*?>/ ------> 非贪婪模式 ------> 只匹配 <h1> </h1>
exp1(?=exp2) 匹配exp2之前的exp1
exp1(?!exp2) 匹配后面不是exp2的exp1
(?<=exp2)exp1  匹配exp2之后的exp1
(?<!exp2)exp1  匹配前面不是exp2的exp1
?:	匹配但是获取匹配结果 例如：abc(?d|e) ----> 等价于abcd|abce
```

正则表达式的修饰符

```javascript
i 	不区分大小写
g 	全局匹配
m	多行匹配
s	. 默认情况下匹配除了换行符（\n）之外的任何字符  加上s修饰符之后将包含换行符
```

#### 正则表达式的一些用法

##### 	1.测试字符串是否符合条件 test()	

```javascript
	/\d{11}/.test("1241224112")
	符合条件返回 true 否则返回false
```

##### 	2.切分字符串 split()  

```javascript
	string方法
	"a b c    d".split(/s+/) ----> ['a', 'b', 'c', 'd']
```

##### 	3.分组 exec()

```javascript
	/^(\d{3})-(\d{3,8})$/.('010-12345') ---> ['010-12345', '010', '12345']
	// 匹配失败时返回null
	// 每个小括号里是一组  返回的数组第一个元素是整个匹配的元素
```

##### 	4.match()

```javascript
	string方法 与exec方法用法和返回值一致
```

##### 	5.matchAll()

```javascript
	string方法
    返回一个迭代器（iterator）
```

##### 	6.search()

```javascript
	string方法 --- 测试匹配的string
	返回匹配的的位置索引 失败时返回 -1
```

##### 	7.replace()

```javascript
	string方法 ---- 查找匹配的字符串并使用替换字符串替换匹配的字符串
    正则后面有修饰符 g 的话会替换所有的匹配项 否则只替换第一个
    $1  $2 代表匹配的第一个第二个子项
    将Doe, John替换为John, Doe
		--> 'Doe, John'.replace(/(\w+)\s*, \s*(\w+)/, "$2 $1");
```

###  一些方法

```javascript
for...of
	for...of语句在可迭代对象（包括 Array，Map，Set，String，TypedArray，arguments 对象等等）上创建一个迭代循环，调用自定义迭代钩子，并为每个不同属性的值执行语句

for...in
    for...in语句以任意顺序遍历一个对象的除Symbol以外的可枚举属性。

apply()和call()

apply(arg, arguments) // arg-->需要绑定的this变量    arguments-->参数是Array，表示函数本身的参数
call(arg, ...arguments) // arg-->需要绑定的this变量  arguments-->参数是Array，表示函数本身的参数
// 两者的区别：
	apply()把参数打包成Array再传入；
	call()把参数按顺序传入。
```

##### Array

###### 	1.reduce() 

​		主要就是运行结果和数组的下一个元素继续运算  最后返回一个结果

```javascript
arr.reduce((accumulator, currentValue, currentIndex, arr) => {}, initValue)

accumulator 累计器 就是上一次的运算结果
currentValue 当前值 现在遍历到的数组元素
currentIndex 当前索引 当前元素的索引
array 数组 调用此方法的数组
initValue 初始值
```



##### 箭头函数

​	箭头函数不会创建自己的this 只会从自己的作用链的上一层继承this

​	箭头函数没有自己的`this`，它会捕获自己在**定义时**（注意，是定义时，不是调用时）所处的**外层执行环境的`this`**，并继承这个`this`值。所以，箭头函数中`this`的指向在它被定义的时候就已经确定了，**之后永远不会改变**

​	不能作为构造函数使用

​	箭头函数没有自己的arguments

​	箭头函数没有原型prototype

##### generator

​	generator和函数不同的是，generator由`function*`定义（注意多出的`*`号），并且，除了`return`语句，还可以用`yield`返回多次

​	获取generator返回的多个值的方法

  1. next() 方法

     `next()`方法会执行generator的代码，然后，每次遇到`yield x;`就返回一个对象`{value: x, done: true/false}`，然后“暂停”。返回的`value`就是`yield`的返回值，`done`表示这个generator是否已经执行结束了。如果`done`为`true`，则`value`就是`return`的返回值

  2. for... of 循环

     直接用`for ... of`循环迭代generator对象，这种方式不需要我们自己判断`done`

     这个循环会直接拿出每次返回的值

     ```javascript
     function* counter(x) {
         yield x + 1;
         yield x + 2;
         yield x + 3;
     }
     
     for (const r of counter(1)) {
         console.log(r)
     }
      
     // 2
     // 3
     // 4
     ```

     

​	

