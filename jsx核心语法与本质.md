## JSX简介
JSX是一种JavaScript的语法扩展（extension），用于描述UI界面，和JavaScript融合在一起使用
React认为渲染逻辑本质上与其他UI逻辑存在耦合比如UI需要绑定事件（button、a原生等等）所以React没有将渲染漏记和UI逻辑分离到不同文件，而是组合到一起作为组件（Component）
## JSX的书写规范：
JSX只能有一个根元素，一般会在外层包裹一个div（或Fragment）
通常在jsx外层包裹一个()，方便阅读
JSX中的标签可以是单标签，也可以是双标签。如果是单标签，必须以/>结尾
## JSX嵌入变量
变量是Number、String、Array时，可以直接显示
变量是null、undefined、Boolean时，内容为空
    (如果希望显示，需要转成String，使用toString、和空字符串拼接，String()等方式)
    为什么要显示为空内容呢？因为在开发中经常进行判断，结果为false则不显示一个内容
对象类型不能作为子元素（报错：not valid as a React child）

JSX嵌入动态表达式：{表达式}，表达式可以是运算式，三元表达式，函数等
JSX注释：{/* 我是一段注释 */}
jsx事件监听：
    React 事件命名采用小驼峰式（camelCase），而不是纯小写

## this绑定问题：
``` JavaScript
 class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      message: "你好啊,李银河"
    }
  }

  render() {
    return (
      <div>
        <button onClick={this.btnClick}>点我一下(React)</button>
      </div>
    )
  }

  btnClick() {
    console.log(this);
    console.log(this.state.message);
  }
}
 ```
因为onClick不是主动调用，而是React内部在监听到btn被点击时调用，因此this无法被正确绑定
解决方式：
1.bind()：btnClick().bind(this)
2.class fields 语法：btnClick = () => {xxx}，这是es6给类定义属性的方法
3.onClick传入箭头函数：onClick={() => this.btnClick()}

## 事件参数传递
直接传入箭头函数即可获取event对象
若想获取更多的参数，可以传入箭头函数之后主动执行，并传入想要获取的参数
``` JavaScript
class App extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      names: ["衣服", "鞋子", "裤子"]
    }
  }

  render() {
    return (
      <div>
        {/* 直接传入箭头函数即可获取event对象 */}
        <a href="http://www.baidu.com" onClick={this.aClick}>点我一下</a>
        {
          this.state.names.map((item, index) => {
            return (
              {/* 若想获取更多的参数，可以传入箭头函数之后主动执行，并传入想要获取的参数 */}
                <a href="#" onClick={e => this.aClick(e, item, index)}>{item}</a>
            )
          })
        }
      </div>
    )
  }

  aClick(e, item, index) {
    e.preventDefault();
    console.log(item, index);
    console.log(e);
  }
}
 ```

## 条件渲染
### 1.条件判断语句
``` JavaScript
class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isLogin: true
    }
  }

  render() {
    return (
      <div>
        {this.getTitleJsx()}
      </div>
    )
  }

  getTitleJsx() {
    let titleJsx = null;
    if (this.state.isLogin) {
      titleJsx = <h2>欢迎回来~</h2>
    } else {
      titleJsx = <h2>请先登录~</h2>
    }
    return titleJsx;
  }
} 
```

### 2.与运算符&& （）
`{this.state.isLogin && <h2>{this.state.username}</h2>}`
三元表达式尽量避免使用
## 列表渲染
在React中，展示列表使用最多的方式是map()
`arr.map(function callback(currentValue[, index[, array]])`

## JSX原理解析
jsx是React.createElement(component, props, ...children)的**语法糖**
`createElement(type, config, children)`
**type**: ReactElement的类型,
**config**: 所有jsx的属性都在config中以对象形式存储
**children**: 存放在标签中的内容，以children数组存储, props.children

jsx通过babel进行转换

## 虚拟DOM
ReactElement对象的作用：React利用ReactElement对象组成了一个JavaScript的对象树，即虚拟DOM（Virtual DOM）
**虚拟DOM的意义**
1.原始操作DOM，状态难以跟踪(debug调试，console.log)，虚拟DOM容易跟踪
2.频繁操作真实DOM，影响性能，因为真实DOM具有复杂属性；容易引起浏览器的回流和重绘

虚拟DOM实现从**命令式编程**转到了**声明式编程**(只需要关注state，React确保state和DOM匹配)
![](2020-12-19-11-23-59.png)

**React渲染流程**：
JSX => (createElement) => Virtual DOM  => (render) =>  Real DOM
通过render()将Virtual和Real DOM同步的过程叫做**Reconciliation**
