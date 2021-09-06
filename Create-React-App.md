# Create-React-App

## 一.create-react-app

##### 	1.使用命令创建一个新的空白React项目

```
 npx create-react-app projectName
```

##### 	2.删除无用文件 添加项目的文件结构目录

​		基本目录结构： 
>>>>>>> 0ad3e21d84dd89ddc892f909c01ced188a7b0627

   	![image-20210901165757975](https://user-images.githubusercontent.com/73156828/131849545-1ffcc82f-2b63-4e5c-beba-cc161db0bc1d.png)
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
<<<<<<< HEAD

## 三.axios

#### 1.添加依赖

```javascript
 npm　install axios
```

#### 2.封装axios

第一种

```javascript
import axios from "axios";

const getBaseURL = (env) => {
    // TODO 根据启动的环境不同添加不同的baseURL
    return 'http://localhost:9000'
}
const defaultConfig = {
    baseURL : getBaseURL(process.env.NODE_ENV),
    timeout : 600000,
}

const newAxios = axios.create(defaultConfig);

const authState = window.authState;
// 拦截每一个请求
newAxios.interceptors.request.use(
    // 请求成功时
    config => {
        // 请求加上token
        const { noAuthorization } = config
        if(!noAuthorization) {
            config.headers['Authorization'] = 'Bearer ' + authState.accessToken && authState.accessToken.accessToken
        }
        console.log(config, '请求的config')
        return config
    },error => Promise.reject(error)
)

// 拦截每一个响应
newAxios.interceptors.response.use(
    response => {
        return response
    },
    error => Promise.reject(error)
)

export default newAxios;
```

第二种

```javascript
import axios from 'axios';
import history from '../history';

export const getBaseUrl = (env) => {

  let base = {
    production: process.env.REACT_APP_SERVER || '/',
    development: process.env.REACT_APP_SERVER || 'http://localhost:9000',
    test: process.env.REACT_APP_SERVER || 'http://localhost:9000',
  }[env];
  if (!base) {
    base = '/';
  }
  return base;
};

class NewAxios {
  constructor() {
    this.baseURL = getBaseUrl(process.env.NODE_ENV);
    this.timeout = 600000;
    this.withCredentials = true;
  }

  // 这里的url可供你针对需要特殊处理的接口路径设置不同拦截器。
  setInterceptors = (instance, url, noErrorTip, noRedirect) => {
    instance && instance.interceptors && instance.interceptors.request.use((config) => {
      try {
        return config;
      } catch (e) {
        Promise.reject(e)
      }
    }, err => Promise.reject(err));

    instance && instance.interceptors && instance.interceptors.response.use((response) => {
      // 在这里移除loading
      // todo: 想根据业务需要，对响应结果预先处理的，都放在这里
      console.log(response.responseType)
      return response;
    }, (err) => {
      console.log(err, err.response)
      if (noErrorTip) {
        return;
      }
      if (err.response) { // 响应错误码处理
        switch (err.response.status) {
          case 401:
            // history.push('/401')
            // 登录过期，应该要重新登录获取accessToken
            localStorage.clear()
            window.authService.login()
            break;
          case 403:
            history.push('/403')
            break;
          default:
            // message.info('当前网络问题，请稍后访问！')
            break;
        }
        return Promise.reject(err.response);
      }

      if (!window.navigator.onLine) { // 断网处理
        Promise.reject({
          status: 404
        })
      }

      if (err.message === 'Network Error') {
        !noRedirect && history.push('/error')
        
        return Promise.reject({
          status: 404
        });
      }
      return Promise.reject(err);
    });
  }

  async getToken() {
    return await window.authService && window.authService.getAccessToken()
  }

  async request(options) {
    let token = ''
    await this.getToken().then(res => token = res)
    const config = { // 将用户传过来的参数与公共配置合并。
      baseURL: this.baseURL,
      timeout: this.timeout,
      withCredentials: this.withCredentials,
      ...options,
      headers: token && !options.noAuthorization ? {
        ...options.headers,
        Authorization:  `Bearer ${token}`
      } :{
        ...options.headers
      } 
    };
    const instance = axios.create(config);
    // 配置拦截器，支持根据不同url配置不同的拦截器。
    this.setInterceptors(instance, options.url, options.noErrorTip, options.noRedirect);
    return instance(); // 返回axios实例的执行结果
  }
}

export default new NewAxios();
```

#### 3.封装request请求

```react
import axios from './axios';
import {message} from 'antd';

message.config({
    maxCount : 1,
    getContainer : () => document.getElementById('root')
})

export default function fetchData (config) {

    if (config.cacheName) {
        const data = window.sessionStorage.getItem(config.cacheName);
        if (data && data.length) {
          return Promise.resolve(JSON.parse(data));
        }
    }

    return axios.request(config).then(res => {
        if (!!config.cacheName) {
            window.sessionStorage.setItem(config.cacheName, JSON.stringify(res.data));
        }
        return res.data;
    }).catch(error => {
        // TODO 对于错误的处理 message
    })

}
```

## 四.mock api

#### 1.根目录下添加mock-api文件夹

```
/mock-api
    ...
/public
    ...
/src
    ...
package.json
```

#### 2.添加connect-api-mocker

```
npm i --save-dev express connect-api-mocker
```

#### 3.添加api.js文件

​	在mock-api/api.js

```javascript
const express = require('express');
const apiMocker = require('connect-api-mocker');
// mock 后端server的端口
const port = 9000;
const app = express();
 
app.use('/api', apiMocker('mock-api'));
 
console.log(`Mock API Server is up and running at: http://localhost:${port}`);
app.listen(port);
```

#### 4.根据url添加mock数据文件

```
/mock-api
    /user
        /harvey
            GET.json ------> /user/harvey (get)
        /unauthorised
            GET.json
        /__userName__
            GET.js  -------> /user/{userName} 
```

#### 5.配置跨域

```javascript
// 添加依赖
npm i -D cors
// 修改api.js文件 添加以下代码
const cors = require('cors');
app.use(cors());
```

#### 6.添加启动命令

```javascript
"scripts": {
  ...
  "mock-api": "node ./mock-api/app.js",
  ...
```

```
npm run mock-api // 启动mock的服务
```

## 五.多环境文件的配置

=======
>>>>>>> 0ad3e21d84dd89ddc892f909c01ced188a7b0627
