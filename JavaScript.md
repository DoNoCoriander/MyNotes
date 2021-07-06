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

