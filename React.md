# **REACT**

## 创建React的项目的命令

```
npx create-react-app  projectName
```

## Hooks

#### 1.useContext

​	作用：全局共享数据(方法)  主要用于组件层级较深并且需要向子组件传值  避免使用props一层层的向下传递

```javascript
// 第一步：创建需要共享的context 并可以赋予初始值 创建在父组件中
export const ThemeContext = React.createContext('light');
// 父组件
export function App (){
  render() {
    // 第二步：使用 Provider 提供 ThemeContext 的值，Provider所包含的子树都可以直接访问ThemeContext的值
    return (
      <ThemeContext.Provider value="dark">
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
}

// Toolbar 组件并不需要透传 ThemeContext
export function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}
// 深处的子组件
export function ThemedButton(props) {
  // 第三步：使用共享 Context
  const theme = useContext(ThemeContext);
    return <Button theme={theme} />;
}
```

#### 2.useReducer

用法：对于复杂的state操作逻辑，嵌套的state的对象

基本语法：

```javascript
const [state, dispatch] = useReducer(reducer(函数), initState(初始状态));
```

```react
 // 第一个参数：应用的初始化
    const initialState = {count: 0};

    // 第二个参数：state的reducer处理函数
    function reducer(state, action) {
        switch (action.type) {
            case 'increment':
              return {count: state.count + 1};
            case 'decrement':
               return {count: state.count - 1};
            default:
                throw new Error();
        }
    }

    function Counter() {
        // 返回值：最新的state和dispatch函数
        const [state, dispatch] = useReducer(reducer, initialState);
        return (
            <>
                // useReducer会根据dispatch的action，返回最终的state，并触发render
                Count: {state.count}
                // dispatch 用来接收一个 action参数「reducer中的action」，用来触发reducer函数，更新最新的状态
                <button onClick={() => dispatch({type: 'increment'})}>+</button>
                <button onClick={() => dispatch({type: 'decrement'})}>-</button>
            </>
        );
    }
```

#### 3.useRef

用处 ： 转发组件    转发子组件的值到父组件中

```react
// 父组件
export default function Father () {
    
	const refValue = useRef()
    
    // refValue.current 就是子组件向父组件返回的值
    
    return (
    	<>
        	<Children ref = {refValue}></Children>
        </>
    )
} 

// 子组件
function Children (props, ref) {
    useImperativeHandle(ref, () => ({
        // 子组件要向父组件返回的值
    })[])
}
export default forwardRef(Children)
```

#### 4.useImperativeHandle

向父组件转发子组件的部分值  需要和**useRef**配合使用

基本语法 ：

```react
useImperativeHandle(ref, createHandle, [deps])
```

## REACT动态加载主题

**使用到的依赖 ： less , less-loader , antd-theme-generator**

#### 1.配置less和less-loader

- 安装 customize-cra 和  react-app-rewired

  ```javascript
  npm install customize-cra  react-app-rewired --save-dev
  ```

- 在根目录下创建一个文件名为 config-overrides.js 

  - react-app-rewired    覆盖create-react-app命令的默认配置

  - 在文件中添加：

    ```javascript
    const {
      override,
    } = require('customize-cra');
    
    module.exports = override(
      // 这里我们将实现对默认设置的覆盖条件
    )
    ```

- 修改package.json里的scripts命令：

  ```javascript
   // 修改前
      "start": "react-scripts start",
      "build": "react-scripts build",
      "eject": "react-scripts eject"
  // 修改后
      "start": "react-app-rewired start",
      "build": "react-app-rewired build",
      "eject": "react-scripts eject"
  ```

- 安装less 和 less-loader

  - ```javascript
    npm install less less-loader --save-dev
    ```

    less-loader 版本过高可能会出现错误 推荐使用5.0.0
    
    less版本过高也会出现问题 可以降低为@2.7

- 在config-overrides文件中增加less文件配置：

  ```javascript
  const {
    override,
    addLessLoader,
  } = require('customize-cra');
  
  module.exports = override(
    addLessLoader({  
      lessOptions: { 
        javascriptEnabled: true,
        modifyVars: { '@primary-color': '#1DA57A' },
      },
      sourceMap:true,
    }),
  )
  ```

#### 2.配置antd-theme-generator

- 安装 `antd-theme-generator`

  ```javascript
  npm install --save antd-theme-generator
  ```

- 在根目录下添加`color.js`文件 (**修改文件的路径系统的文件路径对应起来**)

  ```javascript
  const path = require('path');
  const { generateTheme } = require('antd-theme-generator');
  
  const options = {
      stylesDir: path.join(__dirname, "../src/styles"),//样式文件的地址
      antDir: path.join(__dirname, "../node_modules/antd"),
      varFile: path.join(__dirname, "../src/styles/variables.less"),//一些要改变主题色的初始值文件
      mainLessFile: path.join(__dirname, "../src/styles/index.less"),//样式文件的入口
      themeVariables: [ //可以改变的样式
          "@primary-color",
          "@secondary-color",
          "@text-color",
          "@text-color-secondary",
          "@heading-color",
          "@layout-body-background",
          "@layout-header-background",
          "@border-radius-base"
      ],
      outputFilePath: path.join(__dirname, "../public/color.less")//`antd-theme-generator`自动生成的样式文件地址
  };
  
  generateTheme(options)
      .then(less => {
          console.log("Theme generated successfully");
      })
      .catch(error => {
          console.log("Error", error);
      });
  ```

- 在 `src` 下创建文件 `src/styles/index.less` 和 `src/styles/variables.less`，这两个文件用于定义全局的主题样式

#### 3.修改pulic文件夹下的HTML文件

```html
<body>
    <!-- 中间这几行是需要添加的 -->
    <link rel="stylesheet/less" type="text/css" href="/color.less" />
    <script>
        window.less = {
            async: false,
            env: 'production'
        };
    </script>
    <script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/less.js/2.7.2/less.min.js"></script>
    <!-- 中间这几行是需要添加的 -->
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root" ></div>
```

#### 4.动态改变的语法

```react
 window.less.modifyVars(
  {
    '@primary-color': '#aaa',
    '@menu-dark-item-active-bg':'#aaa',
    '@link-color': '#aaa',
    '@text-color':'#aaa',
    '@btn-primary-bg': '#aaa',
  }
)
.then(() => { 
  message.success('主题切换成功')
})
.catch(error => {
  message.error(`主题切换失败`);
  console.log(error)
});
```

#### 问题 ： 改变主题后刷新页面页面的主题会变回原来的样子

​			 	在根组件渲染的时候确定页面的主题

## Redux

redux只能处理同步变化 处理异步需要借助中间件如：redux-thunk,  redux-saga   

简单的业务场景使用thunk 复杂的使用saga

## 关于antd

1.antd的国际化 但是日期组件的星期和月份还是英语问题

```react
import zhCN from "antd/lib/locale/zh_CN";
import "moment/locale/zh-cn" //加上这么一句即可 // 或者使用yarn install moment不要使用npm
<ConfigProvider locale = {zhCN}>
    <App location = {window.location} />
</ConfigProvider>
```

## 关于文件

**content-type**  ：浏览器会根据这个的值来决定对文件url的处理方式是预览还是下载

### 一些方法

#### 1.react格式化日期：

- 引入插件moment

```js
npm install moment --save
```

- 引入moment 并调用format方法

```js
import moment from 'moment'
当前时间：moment().format('YYYY-MM-DD HH:mm:ss')
时间格式化：moment(datetime).format('YYYY-MM-DD')
```

#### 2.身份证的校验