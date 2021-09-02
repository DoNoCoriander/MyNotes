# Create-React-App

## 一.create-react-app

##### 	1.使用命令创建一个新的空白React项目

```
 npx create-react-app projectName
```

##### 	2.删除无用文件 添加项目的文件结构目录

​		基本目录结构： 		

![image-20210901165757975](C:\Users\sqoz2t6\AppData\Roaming\Typora\typora-user-images\image-20210901165757975.png)    	

##### 3.antd

```
npm install antd
```

​	引入antd的样式

```
import 'antd/dist/antd.css';
```

## 二.Router 添加路由

#### 1.react-router-dom

```javascript
 npm install react-router-dom // 添加router插件
```

```javascript
// 推荐使用 BrowserRouter 作为Router根标签
import { Route, Switch, BrowserRouter as  Router} from "react-router-dom";
```

#### 2.Route

​	Route渲染组件的方式

1. children属性 （Function）

2.  render属性 （Function）
3.  component属性 (Object/Function)
   直接传入组件的话 推荐使用此属性
   如果**component设置的是一个内联函数，每次渲染你都将创建一个新的组件**。每次更新，都存在组件的卸载和挂载,如果使用内联函数进行渲染的话，使用render或children
   同时使用这三个属性 ：
   渲染的优先级 **children > component > render**

#### 3.history 

```javascript
// 使用BrowserRouter路由时
const history = useHistory();

// 使用Router路由时
import { createBrowserHistory } from "history";
const history = createBrowserHistory();
export default history;
```

#### 4.V5的路由嵌套

​	使用**BrowserRouter**

```html
// 父路由
<BrowserRouter>
    <Switch>
       <Route path='/' exact component={User2}></Route>
       <Route key='1' path='/users'>
              <PBOCLayout></PBOCLayout>
       </Route>
    </Switch>
<BrowserRouter/>
    
// 子路由
// 在PBOCLayout组件中
    <Header></Header>
     <div>
         <Switch>
             <Route path='/users/1' component= {Test}></Route>
             <Route path='/users/test' exact component={Test}></Route>
             <Route path='/users/2' exact component={User}></Route>
         </Switch>
     </div>
```

**注意：**

1. 父路由不能添加exact=true, 否则将匹配不到子组件
2. 子组件的path前面需要和父组件一致，需要先匹配到父组件才能匹配到子组件