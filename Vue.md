# VUE

##### 1.router的函数跳转参数

###### params方式

```vue
this.$router.push({
	name : '', // 组件在routes/index.js中注册时的name属性
	params : {
		// 参数
	}
})
```

###### query方式

```
this.$router.push({
	path : '', // 组件注册时的path属性
	query : {
		// 参数
	}
})
```

被跳转组件的获取参数

```
this.$route.params
this.$route.query
```

