# React

<a name="R9gyC"></a>
# 一.开发依赖
<a name="Ov223"></a>
## 1.开发React必须依赖三个库：

- react：包含react所必须的核心代码
- react-dom：react渲染在不同平台所需要的核心代码
- babel：将jsx转换成React代码的工具
<a name="hyxBL"></a>
## 2.三个库是各司其职：

- 在React的0.14版本之前是没有react-dom这个概念的，所有功能都包含在react里
- 为什么要进行拆分呢？原因就是react-native。
- react包中包含了react和react-native所共同拥有的核心代码。
- react-dom针对web和native所完成的事情不同：
   - web端：react-dom会讲jsx最终渲染成真实的DOM，显示在浏览器中
   - native端：react-dom会讲jsx最终渲染成原生的控件（比如Android中的Button，iOS中的UIButton）
<a name="umSjt"></a>
## 3.babel是什么呢？

- Babel ，又名 Babel.js。
- 是目前前端使用非常广泛的编辑器、转移器。
- 当下很多浏览器并不支持ES6的语法，开发时希望使用ES6。
- 那么编写源码时我们就可以使用ES6来编写，之后通过Babel工具，将ES6转成大多数浏览器都支持的ES5的语法。
<a name="kXlPr"></a>
## 4.React和Babel的关系：

- 默认情况下开发React其实可以不使用babel。
- 但是前提是我们自己使用 React.createElement 来编写源代码，它编写的代码非常的繁琐和可读性差。
- 那么我们就可以直接编写jsx（JavaScript XML）的语法，并且让babel帮助我们转换成React.createElement。
<a name="hZQOM"></a>
## 5.必须添加 type="text/babel"：<br />
```jsx
//作用是可以让babel解析jsx的语法
<script type="text/babel">    // 通过ReactDom对象来渲染内容
    ReactDOM.render(<h2>Hello World</h2>, document.getElementById("app"));
</script>
```
<a name="B03tQ"></a>
## 6.ReactDOM.render函数：

   - 参数一：传递要渲染的内容，这个内容可以是HTML元素，也可以是React的组件
   - 参数二：将渲染的内容，挂载到哪一个HTML元素上，这里使用原生的getElementById()
<a name="WMNpG"></a>
## 7.通过{}引入外部的变量或者表达式
<br />
```jsx
let message = "Hello World";
ReactDOM.render(<h2>{message}</h2>, document.getElementById("app"));
```
<a name="WcmJM"></a>
## 8.在React中，如何封装一个组件呢？

- 这里我们暂时使用类的方式封装组件：
   - render当中返回的jsx内容，就是之后React会帮助我们渲染的内容
   - 1.定义一个类，继承自React.Component
   - 2.实现当前组件的render函数



```jsx
class App extends React.Component {
  render() {
    return (<h2>Hello World</h2>)
  }
}
ReactDOM.render(<App/>, document.getElementById("app"));
```
<a name="qvAfO"></a>
## 9.数据在哪里定义?

- 在组件中的数据，我们可以分成两类：
   - 参与界面更新的数据：当数据变量时，需要更新组件渲染的内容
   - 不参与界面更新的数据：当数据变量时，不需要更新将组建渲染的内容
- 参与界面更新的数据我们也可以称之为是参与数据流，这个数据是定义在当前对象的state中
   - 我们可以通过在构造函数中 this.state = {定义的数据}
- 当我们的数据发生变化时，我们可以调用 this.setState 来更新数据，并且通知React进行update操作
   - 在进行update操作时，就会重新调用render函数，并且使用最新的数据，来渲染界面
<a name="LDkMW"></a>
## 10.事件绑定中的this：

- 在类中直接定义一个函数，并且将这个函数绑定到html原生的onClick事件上，当前这个函数的this指向的是谁呢？
- 默认情况下是undefined
   - 因为在正常的DOM操作中，监听点击，监听函数中的this其实是节点对象（比如说是button对象）；
   - React并不是直接渲染成真实的DOM，我们所编写的button只是一个语法糖，它的本质React的Element对象；
   - 那么在这里发生监听的时候，react给我们的函数绑定的this，默认情况下就是一个undefined；
- 我们在绑定的函数中，可能想要使用当前对象，比如执行 this.setState 函数，就必须拿到当前对象的this
   - 我们就需要在传入函数时，给这个函数直接绑定this
   - 类似于下面的写法：<button onClick={this.changeText.bind(this)}>改变文本</button>
<a name="mVfhe"></a>
# 二.jsx
<a name="fHyta"></a>
## 1.继承
注意：在constructor中，子类必须通过super来调用父类的构造方法，对父类进行初始化，否则会报错。

```jsx
class Student1 extends Person {
  constructor(name, age, sno, score) {
    super(name, age);//父类中的
    this.sno = sno;
    this.score = score;
  }
  studying() {
    console.log(this.name, this.age, this.sno, this.score, "studing");
  }
}
const stu1 = new Student1("wulei", 18, 110, 175);
stu1.studying();
```
<a name="7lxFV"></a>
## 2.JSX是什么？

- JSX是一种JavaScript的语法扩展（eXtension），也在很多地方称之为JavaScript XML，像一段XML语法；
- 它用于描述我们的UI界面，并且其完全可以和JavaScript融合在一起使用；
- 不同于Vue中的模块语法，不需要专门学习模块语法中的一些指令（比如v-for、v-if、v-else、v-bind）；
- 区别于JS和HTML，比如class，需要使用className，因为class在JS中属于类
<a name="HpP8P"></a>
## 3.为什么React选择了JSX？

- React认为渲染逻辑本质上与其他UI逻辑存在内在耦合
   - 比如UI需要绑定事件（button、a原生等等）；
   - 比如UI中需要展示数据状态，在某些状态发生改变时，又需要改变UI；
- 他们之间是密不可分，所以React没有将标记分离到不同的文件中，而是将它们组合到了一起，这个地方就是组件（Component）

JSX的书写规范：

- JSX的顶层**只能有一个根元素**，所以我们很多时候会在外层包裹一个div原生（或者使用后面我们学习的Fragment）；
- 为了方便阅读，我们通常在jsx的外层包裹一个小括号()，这样可以方便阅读，并且jsx可以进行换行书写；
- JSX中的标签可以是单标签，也可以是双标签；
   - 注意：如果是单标签，必须以</>结尾；
<a name="DnvOh"></a>
## 4.JSX嵌入表达式

- 书写规则：{表达式}
- 大括号内可以是变量、字符串、数组、函数调用等任意js表达式；
<a name="jxvRk"></a>
## 5. jsx中的注释
```javascript
<div>
  {/* 我是一段注释 */}
  <h2>Hello World</h2>
</div>
```
<a name="H51h7"></a>
## 6.JSX嵌入变量

- 情况一：当变量是Number、String、Array类型时，可以直接显示
- 情况二：当变量是null、undefined、Boolean类型时，内容为空；
   - 如果希望可以显示null、undefined、Boolean，那么需要转成字符串；
   - 转换的方式有很多，比如toString方法、和空字符串拼接，String(变量)等方式；
- 情况三：对象类型不能作为子元素（not valid as a React child）
<a name="JFJHv"></a>
## 7.为什么null、undefined、Boolean在JSX中要显示为空内容呢？
原因是在开发中，我们会进行很多的判断；

- 在判断结果为false时，不显示一个内容；
- 在判断结果为true时，显示一个内容；
- vue采用自己封装的指令，React相对比较灵活，自己来实现
<a name="027Zi"></a>
## 8.JSX嵌入表达式

- 运算表达式
- 三元运算符
- 执行一个函数



```jsx
{/* 运算表达式 */}
<h2>{this.state.firstName + " " + this.state.lastName}</h2>
{/* 三元运算符 */}
<h2>{this.state.age >= 18 ? "成年人": "未成年人"}</h2>
{/* 执行一个函数 */}
<h2>{this.sayHello("kobe")}</h2>
```
<a name="d8Ygb"></a>
## 9.jsx绑定属性
很多时候，描述的HTML原生会有一些属性，而我们希望这些属性也是动态的：

- 比如元素都会有title属性
- 比如img元素会有src属性
- 比如a元素会有href属性
- 比如元素可能需要绑定class
   - 注意：绑定class比较特殊，因为class在js中是一个关键字，所以jsx中不允许直接写class
   - 写法：使用className替代
- 比如原生使用内联样式style
   - style后面跟的是一个对象类型，对象中是样式的属性名和属性值；
   - 注意：这里会讲属性名转成驼峰标识，而不是连接符-；
<a name="r22dn"></a>
## 10.jsx事件监听

- React 事件的命名采用小驼峰式（camelCase），而不是纯小写；
- 我们需要通过{}传入一个事件处理函数，这个函数会在事件发生时被执行；



```jsx
class App extends React.Component {
  render() {
    return (
      <div>
       <button onClick={this.btnClick}>点我一下(React)</button>
     </div>
    )
  }
 btnClick() {
    console.log("React按钮点击了一下")
  }
}
```


<a name="imRvT"></a>
## 11. this绑定问题

- 比如我们这里打印：this.state.message
   - 但是这里会报错：Cannot read property 'state' of undefined
   - 原因是this在这里是undefined
- 如果我们这里直接打印this，也会发现它是一个undefined
- 原因是btnClick函数并不是我们主动调用的，而且当button发生改变时，React内部调用了btnClick函数；
- 而它内部调用时，并不知道要如何绑定正确的this；
<a name="MMzpY"></a>
## 12.如何解决this的问题呢？
<a name="lERFo"></a>
### 方案一：bind给btnClick显示绑定this
在传入函数时，我们可以主动绑定this：

- 这里我们主动将btnClick中的this通过bind来进行绑定（显示绑定）
- 那么之后React内部调用btnClick函数时，就会有一个this，并且是我们绑定的this；



```jsx
<button onClick={this.btnClick.bind(this)}>点我一下(React)</button>
```


还可以通过在构造方法中直接给this.btnClick绑定this来解决：<br />

```jsx
class App extends React.Component{
  constructor(){
  	super();
    this.btnClick = this.btnClick.bind(this);
  }
  render() {
  	return()
  }
}
```
<a name="j1i6i"></a>
### 方案二：使用 ES6 class fields 语法

- 这是ES6中给类定义属性的方法，称之为class fields语法；
- 箭头函数，在当前函数中的this会去上一个**作用域**中查找；
- 而上一个作用域中的this就是当前的对象；



```jsx
btnClick = () => {
    console.log(this);
    console.log(this.state.message);
}
```
<a name="nDX81"></a>
### 方案三：事件监听时传入箭头函数（推荐）
因为 onClick 中要求我们传入一个函数，那么我们可以直接定义一个箭头函数传入：

- 传入的箭头函数的函数体是我们需要执行的代码，我们直接执行 this.btnClick()；
- this.btnClick()中通过this来指定会进行隐式绑定，最终this也是正确的；



```jsx
<button onClick={() => this.btnClick()}>点我一下(React)</button>
<button onClick={() => this.btnClick()}>也点我一下(React)</button>
```
<a name="MpnYr"></a>
## 13.事件参数传递
在执行事件函数时，有可能我们需要获取一些参数信息：比如event对象、其他参数<br />情况一：获取event对象

- 很多时候我们需要拿到event对象来做一些事情（比如阻止默认行为）
- 假如我们用不到this，那么直接传入函数就可以获取到event对象；

获取更多参数

- 有更多参数时，我们最好的方式就是传入一个箭头函数，主动执行的事件函数，并且传入相关的其他参数；



```jsx
<a href="#" onClick={e => this.aClick(e, item, index)}>{item}</a>
aClick(e, item, index) {
    e.preventDefault();
    console.log(item, index);
    console.log(e);
}
```
 
<a name="OGYZP"></a>
## 14.与运算符&&

- 如果条件成立，渲染某一个组件；
- 如果条件不成立，什么内容也不渲染；

**逻辑与&&**<br />**
```jsx
{this.state.isLogin && <h2>{this.state.username}</h2>}
实现v-show
 const nameDisplay = isLogin ? "block": "none";
 <h2 style={{display: nameDisplay}}>{username}</h2>
```


<a name="9JArP"></a>
## 15.列表渲染

- 在React中，展示列表最多的方式就是使用数组的map高阶函数；
- 当然还有filter，reduce

数组的map函数语法如下：

- callback：生成新数组元素的函数，使用三个参数：
   - currentValue<br />callback 数组中正在处理的当前元素。
   - index可选<br />callback 数组中正在处理的当前元素的索引。
   - array可选<br />map 方法调用的数组。
- thisArg可选：执行 callback 函数时值被用作this。
<a name="0bzPr"></a>
## 16.数组处理
```jsx
this.state.numbers.filter(item => item >= 50).slice(0, 3).map(item => {
     return <li>{item}</li>
}
```
<a name="sO0Z6"></a>
## 17. JSX转换本质
jsx 仅仅只是 React.createElement(component, props, ...children) 函数的语法糖。

- 所有的jsx最终都会被转换成React.createElement的函数调用。

createElement需要传递三个参数：

- 参数一：type
   - 当前ReactElement的类型；
   - 如果是标签元素，那么就使用字符串表示 “div”；
   - 如果是组件元素，那么就直接使用组件的名称；
- 参数二：config
   - 所有jsx中的属性都在config中以对象的属性和值的形式存储
- 参数三：children
   - 存放在标签中的内容，以children数组的方式进行存储；
   - 当然，如果是多个元素呢？React内部有对它们进行处理，处理的源码在下方

对children进行的处理：

- 从第二个参数开始，将其他所有的参数，放到props对象的children中
<a name="p6t2v"></a>
## 18.虚拟DOM
我们通过 React.createElement 最终创建出来一个 ReactElement对象：

- 原因是React利用ReactElement对象组成了一个JavaScript的对象树；
- JavaScript的对象树就是大名鼎鼎的虚拟DOM（Virtual DOM）；

JSX---->ReactElement---->真实DOM<br />为什么要采用虚拟DOM，而不是直接修改真实的DOM呢？

- 很难跟踪状态发生的改变：原有的开发模式，我们很难跟踪到状态发生的改变，不方便针对我们应用程序进行调试；
- 操作真实DOM性能较低：传统的开发模式会进行频繁的DOM操作，而这一的做法性能非常的低；

**虚拟DOM帮助我们从命令式编程转到了声明式编程的模式**<br />React官方的说法：Virtual DOM 是一种编程理念。<br />在这个理念中，UI以一种理想化或者说虚拟化的方式保存在内存中，并且它是一个相对简单的JavaScript对象，我们可以通过ReactDOM.render让 虚拟DOM 和 真实DOM同步起来，这个过程中叫做协调（Reconciliation）；<br />这种编程的方式赋予了React声明式的API：你只需要告诉React希望让UI是什么状态，React来确保DOM和这些状态是匹配的。<br />你不需要直接进行DOM操作，只可以从手动更改DOM、属性操作、事件处理中解放出来；
<a name="Pi746"></a>
# 三.脚手架(create-react-app)
注意：项目名称不能包含大写字母

| Npm | Yarn |
| :--- | :--- |
| npm install | yarn install |
| npm install [package] | yarn add [package] |
| npm install --save [package] | yarn add [package] |
| npm install --save-dev [package] | yarn add [package] [--dev/-D] |
| npm rebuild | yarn install --force |
| npm uninstall [package] | yarn remove [package] |
| npm uninstall --save [package] | yarn remove [package] |
| npm uninstall --save-dev [package] | yarn remove [package] |
| npm uninstall --save-optional [package] | yarn remove [package] |
| npm cache clean | yarn cache clean |
| rm -rf node_modules && npm install | yarn upgrade |


<br />test-react<br />├─ README.md // readme说明文档<br />├─ package.json // 对整个应用程序的描述：包括应用名称、版本号、一些依赖包、以及项目的启动、打包等等（node管理项目必备文件）<br />├─ public<br />│    ├─ favicon.ico // 应用程序顶部的icon图标<br />│    ├─ index.html // 应用的index.html入口文件<br />│    ├─ logo192.png // 被在manifest.json中使用<br />│    ├─ logo512.png // 被在manifest.json中使用<br />│    ├─ manifest.json // 和Web app配置相关<br />│    └─ robots.txt // 指定搜索引擎可以或者无法爬取哪些文件<br />├─ src<br />│    ├─ App.css // App组件相关的样式<br />│    ├─ App.js // App组件的代码文件<br />│    ├─ App.test.js // App组件的测试代码文件<br />│    ├─ index.css // 全局的样式文件<br />│    ├─ index.js // 整个应用程序的入口文件<br />│    ├─ logo.svg // 刚才启动项目，所看到的React图标<br />│    ├─ serviceWorker.js // 默认帮助我们写好的注册PWA相关的代码<br />│    └─ setupTests.js // 测试初始化文件<br />└─ yarn.lock
<a name="NLEj8"></a>
# 四.组件化
<a name="W53Np"></a>
## 1.组件类型

- 根据组件的定义方式，可以分为：函数组件(Functional Component )和类组件(Class Component)；
- 根据组件内部是否有状态需要维护，可以分成：无状态组件(Stateless Component )和有状态组件(Stateful Component)；
- 根据组件的不同职责，可以分成：展示型组件(Presentational Component)和容器型组件(Container Component)；

这些概念有很多重叠，但是他们最主要是关注数据逻辑和UI展示的分离：

- 函数组件、无状态组件、展示型组件主要关注UI的展示；
- 类组件、有状态组件、容器型组件主要关注数据逻辑；
<a name="avkZ1"></a>
## 2.创建React组件
<a name="QXjcf"></a>
### 1.类组件：

- 类组件需要继承自 React.Component
- 类组件必须实现render函数

在ES6之前，可以通过create-react-class 模块来定义类组件，但是目前官网建议我们使用ES6的class类定义。<br />使用class定义一个组件：

- constructor是可选的，我们通常在constructor中初始化一些数据；
- this.state中维护的就是我们组件内部的数据；
- render() 方法是 class 组件中唯一必须实现的方法；

<br />
```jsx
import React, { Component } from 'react';
export default class App extends Component {
  constructor() {
    super();
    this.state = {      
    }
  }
  render() {
    return <h2>Hello App</h2>
  }
}
```

<br />当 `render` 被调用时，它会检查 this.props 和 this.state 的变化并返回以下类型之一：

- **React 元素**：
   - 通常通过 JSX 创建。
   - 例如，<div /> 会被 React 渲染为 DOM 节点，<MyComponent />会被 React 渲染为自定义组件；
   - 无论是 <div /> 还是 <MyComponent /> 均为 React 元素。
- **数组或 fragments**：使得 render 方法可以返回多个元素。
- **Portals**：可以渲染子节点到不同的 DOM 子树中。
- **字符串或数值类型**：它们在 DOM 中会被渲染为文本节点
- **布尔类型或 **null：什么都不渲染。
<a name="tMOw5"></a>
### 2.创建函数组件
函数组件是使用function来进行定义的函数，只是这个函数会返回和类组件中render函数返回一样的内容。<br />函数组件有自己的特点，相对于类组件更加简单便捷：

- 没有生命周期，也会被更新并挂载，但是没有生命周期函数；
- 没有this(组件实例）；
- 没有内部状态（state）；

<br />
```javascript
export default function App() {
  return (
    <div>Hello World</div>
  )
}
```


<a name="7Blo2"></a>
## 3.组件的生命周期
生命周期：在合适的地方和时间内完成我们想要实现的效果

- 生命周期是一个抽象的概念，在生命周期的整个过程，分成了很多个阶段；
   - 比如装载阶段（Mount），组件第一次在DOM树中被渲染的过程；
   - 比如更新过程（Update），组件状态发生变化，重新更新渲染的过程；
   - 比如卸载过程（Unmount），组件从DOM树中被移除的过程；
- React内部为了告诉我们当前处于哪些阶段，会对我们组件内部实现的某些函数进行回调，这些函数就是生命周期函数：
   - 比如实现componentDidMount函数：组件已经挂载到DOM上时，就会回调；
   - 比如实现componentDidUpdate函数：组件已经发生了更新时，就会回调；
   - 比如实现componentWillUnmount函数：组件即将被移除时，就会回调；
   - 我们可以在这些回调函数中编写自己的逻辑代码，来完成自己的需求功能；


<br />![微信图片_20200902161505.jpg](https://cdn.nlark.com/yuque/0/2020/jpeg/1575183/1599034565369-d35c3ce3-cc9d-40d4-8012-89634d1a5f7c.jpeg#align=left&display=inline&height=393&margin=%5Bobject%20Object%5D&name=%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20200902161505.jpg&originHeight=393&originWidth=920&size=34805&status=done&style=none&width=920)<br />上图第一个区域解析：

- 当我们挂载一个组件时，会先执行constructor构造方法来创建组件；
- 紧接着调用render函数，获取要渲染的DOM结构（jsx），并且开始渲染DOM；
- 当组件挂载成功（DOM渲染完成），会执行componentDidMount生命周期函数；

上图第二个区域解析：

- 当我们通过修改props，或者调用setState修改内部状态，或者直接调用forceUpdate时会重新调用render函数，进行更新操作；
- 当更新完成时，会回调componentDidUpdate生命周期函数；

上图第三个区域解析：

- 当我们的组件不再使用，会被从DOM中移除掉（卸载）；
- 这个时候会回调componentWillUnmount生命周期函数；

生命周期函数<br />**constructor**<br />constructor(props)<br />如果不初始化 state 或不进行方法绑定，则不需要为 React 组件实现构造函数。<br />constructor中通常只做两件事情：

- 通过给 this.state 赋值对象来初始化内部的state；
- 为事件绑定实例（this）；

**componentDidMount**<br />componentDidMount() 会在组件挂载后（插入 DOM 树中）立即调用。<br />componentDidMount中通常进行哪里操作呢？

- 依赖于DOM的操作可以在这里进行；
- 在此处发送网络请求就最好的地方；（官方建议）
- 可以在此处添加一些订阅（会在componentWillUnmount取消订阅）；

**componentDidUpdate**<br />componentDidUpdate(prevProps, prevState, snapshot)<br />componentDidUpdate() 会在更新后会被立即调用，首次渲染不会执行此方法。

- 当组件更新后，可以在此处对 DOM 进行操作；
- 如果你对更新前后的 props 进行了比较，也可以选择在此处进行网络请求；（例如，当 props 未发生变化时，则不会执行网络请求）。

**componentWillUnmount**<br />componentWillUnmount() 会在组件卸载及销毁之前直接调用。

- 在此方法中执行必要的清理操作；
- 清除 timer，取消网络请求或清除在 componentDidMount() 中创建的订阅等；
<a name="qUvZg"></a>
## 4.不常用生命周期
除了上面介绍的生命周期函数之外，还有一些不常用的生命周期函数：

- getDerivedStateFromProps：state 的值在任何时候都依赖于 props时使用；该方法返回一个对象来更新state；
- getSnapshotBeforeUpdate：在React更新DOM之前回调的一个函数，可以获取DOM更新前的一些信息（比如说滚动位置）；
- shouldComponentUpdate：进行性能优化
<a name="3A6LF"></a>
# 五.组件通信
<a name="T02yX"></a>
## 1.父传子
<a name="NMS91"></a>
### 1.子组件是class组件


```jsx
import React, { Component } from 'react';

// 1.类子组件
class ChildCpn1 extends Component {
  constructor(props) {
    super();
    //通过props来进行传递
    //React在这里默认对props进行了一次绑定
    //写和不写都可以生效
    this.props = props;
  }

  render() {
    //ES6中对象的解构
    const { name, age, height } = this.props;

    return (
      <div>
        <h2>我是class的组件</h2>
        <p>展示父组件传递过来的数据: {name + " " + age + " " + height}</p>
      </div>
    )
  }
}

export default class App extends Component {
  render() {
    return (
      <div>
        <ChildCpn1 name="why" age="18" height="1.88" />
      </div>
    )
  }
}
```


<a name="3eXu1"></a>
### 2.子组件是function组件


```jsx
function ChildCpn2(props) {
  //不需要有构造方法，也不需要有this的问题
  const {name, age, height} = props;

  return (
    <div>
      <h2>我是function的组件</h2>
      <p>展示父组件传递过来的数据: {name + " " + age + " " + height}</p>
    </div>
  )
}

export default class App extends Component {
  render() {
    return (
      <div>
        <ChildCpn1 name="why" age="18" height="1.88"/>
        <ChildCpn2 name="kobe" age="30" height="1.98"/>
      </div>
    )
  }
}
```


<a name="tzRpi"></a>
### 3.参数验证propTypes
对于传递给子组件的数据，有时候我们可能希望进行验证，特别是对于大型项目来说：

- 当然，如果你项目中默认继承了Flow或者TypeScript，那么直接就可以进行类型验证；
- 但是，即使我们没有使用Flow或者TypeScript，也可以通过 prop-types 库来进行参数验证；

从 React v15.5 开始，React.PropTypes 已移入另一个包中：prop-types 库<br />

```jsx
ChildCpn1.propTypes = {
  name: PropTypes.string.isRequired,
  age: PropTypes.number.isRequired,
  height: PropTypes.number.isRequired
}
```


```jsx
ChildCpn1.defaultProps = {
  name: "wulei",
  age: 22,
  height: 1.72
}
```


<a name="RwHZn"></a>
## 2.子传父
<a name="1n0T8"></a>
### 1.某些情况，我们也需要子组件向父组件传递消息：

- 在React中同样是通过props传递消息，只是让父组件给子组件传递一个回调函数，在子组件中调用这个函数即可；
<a name="XpvRy"></a>
### 2.案例实现
子组件通过按钮控制父组件中的数字变化
```jsx
import React, { Component } from 'react';

function CounterButton(props) {
  const { operator, btnClick } = props;
  return <button onClick={btnClick}>{operator}</button>
}

export default class App extends Component {
  constructor(props) {
    super(props);

    this.state = {
      counter: 0
    }
  }

  changeCounter(count) {
    this.setState({
      counter: this.state.counter + count
    })
  }

  render() {
    return (
      <div>
        <h2>当前计数: {this.state.counter}</h2>
        <CounterButton operator="+1" btnClick={e => this.changeCounter(1)} />
        <CounterButton operator="-1" btnClick={e => this.changeCounter(-1)} />
      </div>
    )
  }
}
```
<a name="ocXV5"></a>
## 3.React插槽实现
抽离类似的组件，但是不把里面的东西写死，而是留下一个位置，让使用者可以传入自己想使用的东西，vue中也有类似概念，但是React使用起来更加灵活
<a name="elTbg"></a>
### 1.children实现
每个组件都可以获取到 props.children：它包含组件的开始标签和结束标签之间的内容。<br />比如：<br />

```jsx
<Welcome>Hello world!</Welcome>
```


```jsx
function Welcome(props) {
  return <p>{props.children}</p>;
}
```

<br />利用children属性，我们可以实现以下结构<br />

```jsx
import React, { Component } from 'react';

class NavBar extends Component {
  render() {
    return (
      <div className="nav-bar">
        <div className="item left">{this.props.children[0]}</div>
        <div className="item center">{this.props.children[1]}</div>
        <div className="item right">{this.props.children[2]}</div>
      </div>
    )
  }
}

export default class App extends Component {
  render() {
    return (
      <div>
        <NavBar>
          <div>返回</div>
          <div>购物街</div>
          <div>更多</div>
        </NavBar>
      </div>
    )
  }
}
```
<a name="ZSOp6"></a>
### 2.props实现
通过children实现的方案虽然可行，但是有一个弊端：通过索引值获取传入的元素很容易出错，不能精准的获取传入的原生；<br />另外一个种方案就是使用 props 实现：
```jsx
import React, { Component } from 'react';

class NavBar extends Component {
  render() {
    const { leftSlot, centerSlot, rightSlot } = this.props;

    return (
      <div className="nav-bar">
        <div className="item left">{leftSlot}</div>
        <div className="item center">{centerSlot}</div>
        <div className="item right">{rightSlot}</div>
      </div>
    )
  }
}

export default class App extends Component {
  render() {
    const navLeft = <div>返回</div>;
    const navCenter = <div>购物街</div>;
    const navRight = <div>更多</div>;

    return (
      <div>
        <NavBar leftSlot={navLeft} centerSlot={navCenter} rightSlot={navRight} />
      </div>
    )
  }
} 
```


<a name="fvmJN"></a>
# 六.setState的理解
<a name="B9t2W"></a>
## 1.setState
<a name="MGwCr"></a>
### 1.为什么使用setState
我们是否可以通过直接修改state中的数据来修改界面呢？

- 点击不会有任何反应，为什么呢？
- 因为我们修改了state之后，希望React根据最新的State来重新渲染界面，但是此时React并不知道数据发生了变化；
- React并没有实现类似于Vue2中的Object.defineProperty或者Vue3中的Proxy的方式来监听数据的变化；
- 我们必须通过setState来告知React数据已经发生了变化；
```jsx
changeText() {
    this.state.message = "hello wulei";
}
```
我们必须通过setState来更新数据：

- 疑惑：在组件中并没有实现setState的方法，为什么可以调用呢？
- 原因很简单，setState方法是从Component中继承过来的。
```jsx
Component.prototype.setState = function(partialState, callback) {
  invariant(
    typeof partialState === 'object' ||
      typeof partialState === 'function' ||
      partialState == null,
    'setState(...): takes an object of state variables to update or a ' +
      'function which returns an object of state variables.',
  );
  this.updater.enqueueSetState(this, partialState, callback, 'setState');
};
```
我们可以通过调用setState来修改数据：

- 当我们调用setState时，会重新执行render函数，根据最新的State来创建ReactElement对象；
- 再根据最新的ReactElement对象，对DOM进行修改；
```jsx
changeText() {
  this.setState({
    message: "hello wulei"
  })
}
```
<a name="ZMz1d"></a>
### 2. setState异步更新
我们来看下面的代码：

- 最终打印结果是Hello World；
- 可见setState是异步的操作，我们并不能在执行完setState之后立马拿到最新的state的结果
```jsx
changeText() {
  this.setState({
    message: "hello wulei"
  })
  console.log(this.state.message); // Hello World
}
```
为什么setState设计为异步呢？

- setState设计为异步，可以显著的提升性能；
   - 如果每次调用 setState都进行一次更新，那么意味着render函数会被频繁调用，界面重新渲染，这样效率是很低的；
   - 最好的办法应该是获取到多个更新，之后进行批量更新；
- 如果同步更新了state，但是还没有执行render函数，那么state和props不能保持同步；
   - state和props不能保持一致性，会在开发中产生很多的问题；

那么如何可以获取到更新后的值呢？

- setState接受两个参数：第二个参数是一个回调函数，这个回调函数会在更新后会执行；
- 格式如下：setState(partialState, callback)
```jsx
changeText() {
  this.setState({
    message: "hello wulei"
  }, () => {
    console.log(this.state.message); // hello wulei
  });
}
```
当然，我们也可以在生命周期函数：
```jsx
componentDidUpdate(prevProps, provState, snapshot) {
  console.log(this.state.message);
}
```
<a name="3CDM1"></a>
### 3. setState一定是异步？
疑惑：setState一定是异步更新的吗？<br />验证一：在setTimeout中的更新：
```jsx
changeText() {
  setTimeout(() => {
    this.setState({
      message: "hello wulei"
    });
    console.log(this.state.message); // hello wulei
  }, 0);
}
```
验证二：原生DOM事件：
```jsx
componentDidMount() {
  const btnEl = document.getElementById("btn");
  btnEl.addEventListener('click', () => {
    this.setState({
      message: "hello wulei"
    });
    console.log(this.state.message); // hello wulei
  })
}
```
其实分成两种情况：

- 在组件生命周期或React合成事件中，setState是异步；
- 在setTimeout或者原生dom事件中，setState是同步；
<a name="bqk7q"></a>
### 4. setState的合并
<a name="HmLBZ"></a>
#### 1. 数据的合并
假如我们有这样的数据：
```jsx
this.state = {
  name: "wulei",
  message: "Hello World"
}
```
我们需要更新message：

- 我通过setState去修改message，是不会对name产生影响的；
```jsx
changeText() {
  this.setState({
    message: "hello wulei"
  });
}
```
为什么不会产生影响呢？源码中其实是有对 原对象 和 新对象进行合并的：

- 事实上就是使用 Object.assign(target, ...sources) 来完成的；
<a name="jB4Mt"></a>
#### 2. 多个setState合并
比如我们还是有一个counter属性，记录当前的数字：

- 如果进行如下操作，那么counter会变成几呢？答案是1；
- 为什么呢？因为它会对多个state进行合并；
```jsx
increment() {
    this.setState({
      counter: this.state.counter + 1
    });
    this.setState({
      counter: this.state.counter + 1
    });
    this.setState({
      counter: this.state.counter + 1
    });
  }
```
如何可以做到，让counter最终变成3呢？
```jsx
increment() {
  this.setState((state, props) => {
    return {
      counter: state.counter + 1
    }
  })
  this.setState((state, props) => {
    return {
      counter: state.counter + 1
    }
  })
  this.setState((state, props) => {
    return {
      counter: state.counter + 1
    }
  })
  }
```
为什么传入一个函数就可以变出3呢？

- 原因是多个state进行合并时，每次遍历，都会执行一次函数
- 传入的函数被多次执行
<a name="ZSObv"></a>
## 2. React更新机制
那么React的更新流程呢？<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1600681741938-5978686f-3483-4209-bf2d-834683416eec.webp#align=left&display=inline&height=244&margin=%5Bobject%20Object%5D&originHeight=244&originWidth=709&size=0&status=done&style=none&width=709)<br />React在props或state发生改变时，会调用React的render方法，会创建一颗不同的树。<br />React需要基于这两颗不同的树之间的差别来判断如何有效的更新UI：

- 如果一棵树参考另外一棵树进行完全比较更新，那么即使是最先进的算法，该算法的复杂程度为 O(n 3 )，其中 n 是树中元素的数量；
- 如果在 React 中使用了该算法，那么展示 1000 个元素所需要执行的计算量将在十亿的量级范围；
- 这个开销太过昂贵了，React的更新性能会变得非常低效；

于是，React对这个算法进行了优化，将其优化成了O(n)，如何优化的呢？

- 同层节点之间相互比较，不会跨节点比较；
- 不同类型的节点，产生不同的树结构；
- 开发中，可以通过key来指定哪些节点在不同的渲染下保持稳定；
<a name="O8DFB"></a>
### 1. Diffing算法
<a name="caAcX"></a>
#### 1. 对比不同类型的元素
当节点为不同的元素，React会拆卸原有的树，并且建立起新的树：

- 当一个元素从 `<a>` 变成 `<img>`，从 `<Article>` 变成 `<Comment>`，或从 `<Button>` 变成`<div>` 都会触发一个完整的重建流程；
- 当卸载一棵树时，对应的DOM节点也会被销毁，组件实例将执行`componentWillUnmount()` 方法；
- 当建立一棵新的树时，对应的 DOM 节点会被创建以及插入到 DOM 中，组件实例将执行 `componentWillMount()` 方法，紧接着 `componentDidMount()` 方法；

比如下面的代码更改：

- React 会销毁 `Counter` 组件并且重新装载一个新的组件，而不会对Counter进行复用；
```jsx
<div>
  <Counter />
</div>
<span>
  <Counter />
</span>
```
<a name="2fhUL"></a>
#### 2. 对比同一类型的元素
当比对两个相同类型的 React 元素时，React 会保留 DOM 节点，仅比对及更新有改变的属性。<br />比如下面的代码更改：

- 通过比对这两个元素，React 知道只需要修改 DOM 元素上的 `className` 属性；
```jsx
<div className="before" title="stuff" />
<div className="after" title="stuff" />
```
比如下面的代码更改：

- 当更新 `style` 属性时，React 仅更新有所更变的属性。
- 通过比对这两个元素，React 知道只需要修改 DOM 元素上的 `color` 样式，无需修改 `fontWeight`。
```jsx
<div style={{color: 'red', fontWeight: 'bold'}} />
<div style={{color: 'green', fontWeight: 'bold'}} />
```
如果是同类型的组件元素：

- 组件会保持不变，React会更新该组件的props，并且调用`componentWillReceiveProps()`和 `componentWillUpdate()` 方法；
- 下一步，调用 `render()` 方法，diff 算法将在之前的结果以及新的结果中进行递归；
<a name="4Qnxd"></a>
#### 3. 对子节点进行递归
在默认条件下，当递归 DOM 节点的子元素时，React 会同时遍历两个子元素的列表；当产生差异时，生成一个 mutation。<br />我们来看一下在最后插入一条数据的情况：

- 前面两个比较是完全相同的，所以不会产生mutation；
- 最后一个比较，产生一个mutation，将其插入到新的DOM树中即可；
```javascript
<ul>
  <li>first</li>
  <li>second</li>
</ul>
<ul>
  <li>first</li>
  <li>second</li>
  <li>third</li>
</ul>
```
但是如果我们是在中间插入一条数据：

- React会对每一个子元素产生一个mutation，而不是保持 `<li>星际穿越</li>`和`<li>盗梦空间</li>`的不变；
- 这种低效的比较方式会带来一定的性能问题；
```javascript
<ul>
  <li>星际穿越</li>
  <li>盗梦空间</li>
</ul>
<ul>
  <li>大话西游</li>
  <li>星际穿越</li>
  <li>盗梦空间</li>
</ul>
```
<a name="XEQSL"></a>
### 2. keys的优化
我们在前面遍历列表时，总是会提示一个警告，让我们加入一个key属性：<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1600681741978-f859da9b-5ff6-4e5b-ba51-74156e5b9da4.webp#align=left&display=inline&height=107&margin=%5Bobject%20Object%5D&originHeight=107&originWidth=946&size=0&status=done&style=none&width=946)key的警告<br />我们来看一个案例：
```jsx
import React, { Component } from 'react'
export default class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      movies: ["星际穿越", "盗梦空间"]
    }
  }
  render() {
    return (
      <div>
        <h2>电影列表</h2>
        <ul>
          {
            this.state.movies.map((item, index) => {
              return <li>{item}</li>
            })
          }
        </ul>
        <button onClick={e => this.insertMovie()}>插入数据</button>
      </div>
    )
  }
  insertMovie() {
  }
}
```
方式一：在最后位置插入数据

- 这种情况，有无key意义并不大
```jsx
insertMovie() {
  const newMovies = [...this.state.movies, "大话西游"];
  this.setState({
    movies: newMovies
  })
}
```
方式二：在前面插入数据

- 这种做法，在没有key的情况下，所有的li都需要进行修改；
```javascript
insertMovie() {
  const newMovies = ["大话西游", ...this.state.movies];
  this.setState({
    movies: newMovies
  })
}
```
当子元素(这里的li)拥有 key 时，React 使用 key 来匹配原有树上的子元素以及最新树上的子元素：

- 在下面这种场景下，key为111和222的元素仅仅进行位移，不需要进行任何的修改；
- 将key为333的元素插入到最前面的位置即可；
```javascript
<ul>
  <li key="111">星际穿越</li>
  <li key="222">盗梦空间</li>
</ul>
<ul>
  <li key="333">Connecticut</li>
  <li key="111">星际穿越</li>
  <li key="222">盗梦空间</li>
</ul>
```
key的注意事项：

- key应该是唯一的；
- key不要使用随机数（随机数在下一次render时，会重新生成一个数字）；
- 使用index作为key，对性能是没有优化的；
<a name="K6qBB"></a>
### 3. SCU的优化
<a name="EQzhY"></a>
#### 1. render函数被调用
我们使用之前的一个嵌套案例：

- 在App中，我们增加了一个计数器的代码；
- 当点击+1时，会重新调用App的render函数；
- 而当App的render函数被调用时，所有的子组件的render函数都会被重新调用；
```jsx
import React, { Component } from 'react';
function Header() {
  console.log("Header Render 被调用");
  return <h2>Header</h2>
}
class Main extends Component {
  render() {
    console.log("Main Render 被调用");
    return (
      <div>
        <Banner/>
        <ProductList/>
      </div>
    )
  }
}
function Banner() {
  console.log("Banner Render 被调用");
  return <div>Banner</div>
}
function ProductList() {
  console.log("ProductList Render 被调用");
  return (
    <ul>
      <li>商品1</li>
      <li>商品2</li>
      <li>商品3</li>
      <li>商品4</li>
      <li>商品5</li>
    </ul>
  )
}
function Footer() {
  console.log("Footer Render 被调用");
  return <h2>Footer</h2>
}
export default class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0
    }
  }
  render() {
    console.log("App Render 被调用");
    return (
      <div>
        <h2>当前计数: {this.state.counter}</h2>
        <button onClick={e => this.increment()}>+1</button>
        <Header/>
        <Main/>
        <Footer/>
      </div>
    )
  }
  increment() {
    this.setState({
      counter: this.state.counter + 1
    })
  }
}
```
![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1600681741991-e4bd9c76-af7a-4fe4-a099-fd9128932d6b.webp#align=left&display=inline&height=339&margin=%5Bobject%20Object%5D&originHeight=339&originWidth=592&size=0&status=done&style=none&width=592)嵌套树结构<br />那么，我们可以思考一下，在以后的开发中，我们只要是修改了App中的数据，所有的组件都需要重新render，进行diff算法，性能必然是很低的：

- 事实上，很多的组件没有必须要重新render；
- 它们调用render应该有一个前提，就是依赖的数据（state、props）发生改变时，再调用自己的render方法；

如何来控制render方法是否被调用呢？

- 通过`shouldComponentUpdate`方法即可；
<a name="w8qAl"></a>
#### 2. shouldComponentUpdate
React给我们提供了一个生命周期方法 `shouldComponentUpdate`（很多时候，我们简称为SCU），这个方法接受参数，并且需要有返回值：

- 该方法有两个参数：
   - 参数一：nextProps 修改之后，最新的props属性
   - 参数二：nextState 修改之后，最新的state属性
- 该方法返回值是一个boolean类型
   - 返回值为true，那么就需要调用render方法；
   - 返回值为false，那么久不需要调用render方法；
   - 默认返回的是true，也就是只要state发生改变，就会调用render方法；
```jsx
shouldComponentUpdate(nextProps, nextState) {
  return true;
}
```
我们可以控制它返回的内容，来决定是否需要重新渲染。<br />比如我们在App中增加一个message属性：

- jsx中并没有依赖这个message，那么它的改变不应该引起重新渲染；
- 但是因为render监听到state的改变，就会重新render，所以最后render方法还是被重新调用了；
```jsx
export default class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0,
      message: "Hello World"
    }
  }
  render() {
    console.log("App Render 被调用");
    return (
      <div>
        <h2>当前计数: {this.state.counter}</h2>
        <button onClick={e => this.increment()}>+1</button>
        <button onClick={e => this.changeText()}>改变文本</button>
        <Header/>
        <Main/>
        <Footer/>
      </div>
    )
  }
  increment() {
    this.setState({
      counter: this.state.counter + 1
    })
  }
  changeText() {
    this.setState({
      message: "你好啊,李银河"
    })
  }
}
```
这个时候，我们可以通过实现shouldComponentUpdate来决定要不要重新调用render方法：

- 这个时候，我们改变counter时，会重新渲染；
- 如果，我们改变的是message，那么默认返回的是false，那么就不会重新渲染；
```jsx
shouldComponentUpdate(nextProps, nextState) {
  if (nextState.counter !== this.state.counter) {
    return true;
  }
  return false;
}
```
但是我们的代码依然没有优化到最好，因为当counter改变时，所有的子组件依然重新渲染了：

- 所以，事实上，我们应该实现所有的子组件的shouldComponentUpdate；

比如Main组件，可以进行如下实现：

- `shouldComponentUpdate`默认返回一个false；
- 在特定情况下，需要更新时，我们在上面添加对应的条件即可；
```jsx
class Main extends Component {
  shouldComponentUpdate(nextProps, nextState) {
    return false;
  }
  render() {
    console.log("Main Render 被调用");
    return (
      <div>
        <Banner/>
        <ProductList/>
      </div>
    )
  }
}
```
<a name="L0eRU"></a>
#### 3. PureComponent和memo
如果所有的类，我们都需要手动来实现 shouldComponentUpdate，那么会给我们开发者增加非常多的工作量。<br />我们来设想一下shouldComponentUpdate中的各种判断的目的是什么？

- props或者state中的数据是否发生了改变，来决定shouldComponentUpdate返回true或者false；

事实上React已经考虑到了这一点，所以React已经默认帮我们实现好了，如何实现呢？

- 将class基础自PureComponent。

比如我们修改Main组件的代码：
```jsx
class Main extends PureComponent {
  render() {
    console.log("Main Render 被调用");
    return (
      <div>
        <Banner/>
        <ProductList/>
      </div>
    )
  }
}
```
PureComponent的原理是什么呢？

- 对props和state进行浅层比较；

**查看PureComponent相关的源码：**<br />react/ReactBaseClasses.js中：

- 在PureComponent的原型上增加一个isPureReactComponent为true的属性

![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1600681742039-f0be1c5c-db96-47ce-8917-4db232f14d70.webp#align=left&display=inline&height=617&margin=%5Bobject%20Object%5D&originHeight=617&originWidth=1080&size=0&status=done&style=none&width=1080)PureComponent<br />React-reconcilier/ReactFiberClassComponent.js：<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1600681742067-135f5c2c-aa8f-438a-b984-c1a0ce5a0f57.webp#align=left&display=inline&height=617&margin=%5Bobject%20Object%5D&originHeight=617&originWidth=1080&size=0&status=done&style=none&width=1080)checkShouldComponentUpdate<br />这个方法中，调用 `!shallowEqual(oldProps, newProps) || !shallowEqual(oldState, newState)`，这个shallowEqual就是进行浅层比较：<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1600681742121-b6599ca2-34dc-4682-8306-cc06edd4fc91.webp#align=left&display=inline&height=617&margin=%5Bobject%20Object%5D&originHeight=617&originWidth=1080&size=0&status=done&style=none&width=1080)<br />**那么，如果是一个函数式组件呢？**<br />我们需要使用一个高阶组件memo：

- 我们将之前的Header、Banner、ProductList都通过memo函数进行一层包裹；
- Footer没有使用memo函数进行包裹；
- 最终的效果是，当counter发生改变时，Header、Banner、ProductList的函数不会重新执行，而Footer的函数会被重新执行；
```javascript
import React, { Component, PureComponent, memo } from 'react';
const MemoHeader = memo(function() {
  console.log("Header Render 被调用");
  return <h2>Header</h2>
})
class Main extends PureComponent {
  render() {
    console.log("Main Render 被调用");
    return (
      <div>
        <MemoBanner/>
        <MemoProductList/>
      </div>
    )
  }
}
const MemoBanner = memo(function() {
  console.log("Banner Render 被调用");
  return <div>Banner</div>
})
const MemoProductList = memo(function() {
  console.log("ProductList Render 被调用");
  return (
    <ul>
      <li>商品1</li>
      <li>商品2</li>
      <li>商品3</li>
      <li>商品4</li>
      <li>商品5</li>
    </ul>
  )
})
function Footer() {
  console.log("Footer Render 被调用");
  return <h2>Footer</h2>
}
export default class App extends Component {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0,
      message: "Hello World"
    }
  }
  render() {
    console.log("App Render 被调用");
    return (
      <div>
        <h2>当前计数: {this.state.counter}</h2>
        <button onClick={e => this.increment()}>+1</button>
        <button onClick={e => this.changeText()}>改变文本</button>
        <MemoHeader/>
        <Main/>
        <Footer/>
      </div>
    )
  }
  increment() {
    this.setState({
      counter: this.state.counter + 1
    })
  }
  shouldComponentUpdate(nextProps, nextState) {
    if (nextState.counter !== this.state.counter) {
      return true;
    }
    return false;
  }
  changeText() {
    this.setState({
      message: "你好啊,李银河"
    })
  }
}
```
**memo的原理是什么呢？**<br />react/memo.js：

- 最终返回一个对象，这个对象中有一个compare函数

![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1600681741995-430bfd78-352a-4a64-9225-8281fac16874.webp#align=left&display=inline&height=617&margin=%5Bobject%20Object%5D&originHeight=617&originWidth=1080&size=0&status=done&style=none&width=1080)memo函数
<a name="EE6RX"></a>
#### 4. 不可变数据的力量
我们通过一个案例来演练我们之前说的不可变数据的重要性：
```jsx
import React, { PureComponent } from 'react'
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      friends: [
        { name: "lilei", age: 20, height: 1.76 },
        { name: "lucy", age: 18, height: 1.65 },
        { name: "tom", age: 30, height: 1.78 }
      ]
    }
  }
  render() {
    return (
      <div>
        <h2>朋友列表</h2>
        <ul>
          {
            this.state.friends.map((item, index) => {
              return (
                <li key={item.name}>
                  <span>{`姓名:${item.name} 年龄: ${item.age}`}</span>
                  <button onClick={e => this.incrementAge(index)}>年龄+1</button>
                </li>
              )
            })
          }
        </ul>
        <button onClick={e => this.insertFriend()}>添加新数据</button>
      </div>
    )
  }
  insertFriend() {
     
  }
  incrementAge(index) {
    
  }
}
```
**我们来思考一下inertFriend应该如何实现？**<br />实现方式一：

- 这种方式会造成界面不会发生刷新，添加新的数据；
- 原因是继承自PureComponent，会进行浅层比较，浅层比较过程中两个friends是相同的对象；
```javascript
insertFriend() {
  this.state.friends.push({name: "why", age: 18, height: 1.88});
  this.setState({
    friends: this.state.friends
  })
}
```
实现方式二：

- `[...this.state.friends, {name: "why", age: 18, height: 1.88}]`会生成一个新的数组引用；
- 在进行浅层比较时，两个引用的是不同的数组，所以它们是不相同的；
```javascript
insertFriend() {
  this.setState({
    friends: [...this.state.friends, {name: "why", age: 18, height: 1.88}]
  })
}
```
**我们再来思考一下incrementAge应该如何实现？**<br />实现方式一：

- 和上面方式一类似
```javascript
incrementAge(index) {
  this.state.friends[index].age += 1;
  this.setState({
    friends: this.state.friends
  })
}
```
实现方式二：

- 和上面方式二类似
```javascript
incrementAge(index) {
  const newFriends = [...this.state.friends];
  newFriends[index].age += 1;
  this.setState({
    friends: newFriends
  })
}
```
所以，在真实开发中，我们要尽量保证state、props中的数据不可变性，这样我们才能合理和安全的使用PureComponent和memo。
<a name="3IS9L"></a>
# 七.受控与非受控组件
<a name="2pmUx"></a>
## 1. refs的使用
在React的开发模式中，通常情况下不需要、也不建议直接操作DOM原生，但是某些特殊的情况，确实需要获取到DOM进行某些操作：

- 管理焦点，文本选择或媒体播放。
- 触发强制动画。
- 集成第三方 DOM 库。
<a name="ZRcFh"></a>
### 1. 创建ref的方式
如何创建refs来获取对应的DOM呢？目前有三种方式：

- 方式一：传入字符串
   - 使用时通过 `this.refs.传入的字符串`格式获取对应的元素；
- 方式二：传入一个对象
   - 对象是通过 `React.createRef()` 方式创建出来的；
   - 当然需要首先导入createRef
   - 使用时获取到创建的对象其中有一个`current`属性就是对应的元素；
- 方式三：传入一个函数
   - 该函数会在DOM被挂载时进行回调，这个函数会传入一个 元素对象，我们可以自己保存；
   - 使用时，直接拿到之前保存的元素对象即可；

代码演练：
```jsx
import React, { PureComponent, createRef } from 'react'
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.titleRef = createRef();
    this.titleEl = null;
  }
  render() {
    return (
      <div>
        <h2 ref="title">String Ref</h2>
        <h2 ref={this.titleRef}>Hello Create Ref</h2>
        <h2 ref={element => this.titleEl = element}>Callback Ref</h2>
        <button onClick={e => this.changeText()}>改变文本</button>
      </div>
    )
  }
  changeText() {
    this.refs.title.innerHTML = "hello wulei";
    this.titleRef.current.innerHTML = "hello wulei";
    this.titleEl.innerHTML = "hello wulei";
  }
}
```
<a name="BB5EZ"></a>
### 2. ref节点的类型
ref 的值根据节点的类型而有所不同：

- 当 `ref` 属性用于 HTML 元素时，构造函数中使用 `React.createRef()` 创建的 `ref` 接收底层 DOM 元素作为其 `current` 属性；
- 当 `ref` 属性用于自定义 class 组件时，`ref` 对象接收组件的挂载实例作为其 `current` 属性；
- 你不能在函数组件上使用 ref 属性，因为他们没有实例；

这里我们演示一下ref引用一个class组件对象：<br />class组件案例
```jsx
import React, { PureComponent, createRef } from 'react';
class Counter extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      counter: 0
    }
  }
  render() {
    return (
      <div>
        <h2>当前计数: {this.state.counter}</h2>
        <button onClick={e => this.increment()}>+1</button>
      </div>
    )
  }
  increment() {
    this.setState({
      counter: this.state.counter + 1
    })
  }
}
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.counterRef = createRef();
  }
  render() {
    return (
      <div>
        <Counter ref={this.counterRef}/>
        <button onClick={e => this.increment()}>app +1</button>
      </div>
    )
  }
  increment() {
    this.counterRef.current.increment();
  }
}
```
函数式组件是没有实例的，所以无法通过ref获取他们的实例：

- 但是某些时候，我们可能想要获取函数式组件中的某个DOM元素；
- 这个时候我们可以通过 `React.forwardRef` ；
<a name="o9UCQ"></a>
## 2. 受控组件
<a name="gCfrk"></a>
### 1. 认识受控组件
<a name="vE6k7"></a>
#### 1. 默认提交表单方式
在React中，HTML表单的处理方式和普通的DOM元素不太一样：表单元素通常会保存在一些内部的state。<br />比如下面的HTML表单元素：

- 这个处理方式是DOM默认处理HTML表单的行为，在用户点击提交时会提交到某个服务器中，并且刷新页面；
- 在React中，并没有禁止这个行为，它依然是有效的；
- 但是通常情况下会使用JavaScript函数来方便的处理表单提交，同时还可以访问用户填写的表单数据；
- 实现这种效果的标准方式是使用“受控组件”；
```html
<form>
  <label>
    名字:
    <input type="text" name="name" />
  </label>
  <input type="submit" value="提交" />
</form>
```
<a name="dwbac"></a>
#### 2. 受控组件提交表单
在 HTML 中，表单元素（如`<input>`、 `<textarea>` 和 `<select>`）之类的表单元素通常自己维护 state，并根据用户输入进行更新。<br />而在 React 中，可变状态（mutable state）通常保存在组件的 state 属性中，并且只能通过使用 `setState()`来更新。

- 我们将两者结合起来，使React的state成为“唯一数据源”；
- 渲染表单的 React 组件还控制着用户输入过程中表单发生的操作；
- 被 React 以这种方式控制取值的表单输入元素就叫做“受控组件”；

例如，如果我们想让前一个示例在提交时打印出名称，我们可以将表单写为受控组件：
```jsx
import React, { PureComponent } from 'react'
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      username: ""
    }
  }
  render() {
    const {username} = this.state;
    return (
      <div>
        <form onSubmit={e => this.handleSubmit(e)}>
          <label htmlFor="username">
            用户名: 
            <input type="text" 
                   id="username" 
                   onChange={e => this.handleUsernameChange(e)} 
                   value={username}/>
          </label>
          <input type="submit" value="提交"/>
        </form>
      </div>
    )
  }
  handleUsernameChange(event) {
    this.setState({
      username: event.target.value
    })
  }
  handleSubmit(event) {
    console.log(this.state.username);
    event.preventDefault();
  }
}
```
由于在表单元素上设置了 `value` 属性，因此显示的值将始终为 `this.state.value`，这使得 React 的 state 成为唯一数据源。<br />由于 `handleUsernameChange` 在每次按键时都会执行并更新 React 的 state，因此显示的值将随着用户输入而更新。
<a name="AuElB"></a>
### 2. 常见表单的处理
刚才我们演示的是一个input表单的处理，这里我们再演示一下其他的情况。<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1602205299928-2298627d-0598-4db3-86e0-d021f9cf2b52.webp#align=left&display=inline&height=247&margin=%5Bobject%20Object%5D&originHeight=247&originWidth=920&size=0&status=done&style=none&width=920)<br />表单的处理方式
<a name="lsn9V"></a>
#### 1. textarea标签
texteare标签和input比较相似：
```jsx
import React, { PureComponent } from 'react'
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      article: "请编写你喜欢的文章"
    }
  }
  render() {
    return (
      <div>
        <form onSubmit={e => this.handleSubmit(e)}>
          <label htmlFor="article">
            <textarea id="article" cols="30" rows="10"
                      value={this.state.article}
                      onChange={e => this.handleArticelChange(e)}/>
          </label>
          <div>
            <input type="submit" value="发布文章"/>
          </div>
        </form>
      </div>
    )
  }
  handleArticelChange(event) {
    this.setState({
      article: event.target.value
    })
  }
  handleSubmit(event) {
    console.log(this.state.article);
    event.preventDefault();
  }
}
```
<a name="iTvdg"></a>
#### 2. select标签
select标签的使用也非常简单，只是它不需要通过selected属性来控制哪一个被选中，它可以匹配state的value来选中。<br />我们来进行一个简单的演示：
```jsx
import React, { PureComponent } from 'react'
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      fruits: "orange"
    }
  }
  render() {
    return (
      <div>
        <form onSubmit={e => this.handleSubmit(e)}>
          <label htmlFor="fruits">
            <select id="fruits" 
                    value={this.state.fruits}
                    onChange={e => this.handleFruitsChange(e)}>
              <option value="apple">苹果</option>
              <option value="orange">橘子</option>
              <option value="banana">香蕉</option>
            </select>
          </label>
          <div>
            <input type="submit" value="提交"/>
          </div>
        </form>
      </div>
    )
  }
  handleFruitsChange(event) {
    this.setState({
      fruits: event.target.value
    })
  }
  handleSubmit(event) {
    console.log(this.state.article);
    event.preventDefault();
  }
}
```
<a name="FmOcn"></a>
#### 3. 处理多个输入
多处理方式可以像单处理方式那样进行操作，但是需要多个监听方法：

- 这里我们可以使用ES6的一个语法：计算属性名（Computed property names）
```jsx
let i = 0
let a = {
  ['foo' + ++i]: i,
  ['foo' + ++i]: i,
  ['foo' + ++i]: i
}
console.log(a.foo1) // 1
console.log(a.foo2) // 2
console.log(a.foo3) // 3
let param = 'size'
let config = {
  [param]: 12,
  ['mobile' + param.charAt(0).toUpperCase() + param.slice(1)]: 4
}
console.log(config) // {size: 12, mobileSize: 4}
```
我们进行对应的代码演练
```jsx
import React, { PureComponent } from 'react'
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      username: "",
      password: ""
    }
  }
  render() {
    const {username, password} = this.state;
    return (
      <div>
        <form onSubmit={e => this.handleSubmit(e)}>
          <label htmlFor="username">
            用户: 
            <input type="text" 
                   id="username" 
                   name="username"
                   onChange={e => this.handleChange(e)} 
                   value={username}/>
          </label>
          <label htmlFor="password">
            密码: 
            <input type="text" 
                   id="password" 
                   name="password"
                   onChange={e => this.handleChange(e)} 
                   value={password}/>
          </label>
          <input type="submit" value="提交"/>
        </form>
      </div>
    )
  }
  handleChange(event) {
    this.setState({
      [event.target.name]: event.target.value
    })
  }
  handleSubmit(event) {
    console.log(this.state.username, this.state.password);
    event.preventDefault();
  }
}
```
<a name="JzL6k"></a>
## 3. 非受控组件
React推荐大多数情况下使用 `受控组件` 来处理表单数据：

- 一个受控组件中，表单数据是由 React 组件来管理的；
- 另一种替代方案是使用非受控组件，这时表单数据将交由 DOM 节点来处理；

如果要使用非受控组件中的数据，那么我们需要使用 `ref` 来从DOM节点中获取表单数据。<br />我们来进行一个简单的演练：

- 使用ref来获取input元素；
- 在非受控组件中通常使用defaultValue来设置默认值；
```jsx
import React, { PureComponent, createRef } from 'react'
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.usernameRef = createRef();
  }
  render() {
    return (
      <div>
        <form onSubmit={e => this.handleSubmit(e)}>
          <label htmlFor="">
            用户:<input defaultValue="username" type="text" name="username" ref={this.usernameRef}/>
          </label>
          <input type="submit" value="提交"/>
        </form>
      </div>
    )
  }
  handleSubmit(event) {
    event.preventDefault();
    console.log(this.usernameRef.current.value);
  }
}
```
同样，`<input type="checkbox">` 和 `<input type="radio">` 支持 `defaultChecked`，`<select>` 和 `<textarea>` 支持 `defaultValue`。
<a name="4PInP"></a>
# 
<a name="ipvRR"></a>
# 九、React中的CSS
<a name="B44rv"></a>
## 1. React中的css方案
<a name="8gsWK"></a>
### 1. react中的css
事实上，css一直是React的痛点，也是被很多开发者吐槽、诟病的一个点。<br />在组件化中选择合适的CSS解决方案应该符合以下条件：

- 可以编写局部css：css具备自己的具备作用域，不会随意污染其他组件内的原生；
- 可以编写动态的css：可以获取当前组件的一些状态，根据状态的变化生成不同的css样式；
- 支持所有的css特性：伪类、动画、媒体查询等；
- 编写起来简洁方便、最好符合一贯的css风格特点；
- 等等...

在这一点上，Vue做的要远远好于React：

- Vue通过在.vue文件中编写 `<style><style>` 标签来编写自己的样式；
- 通过是否添加 `scoped` 属性来决定编写的样式是全局有效还是局部有效；
- 通过 `lang` 属性来设置你喜欢的 `less`、`sass`等预处理器；
- 通过内联样式风格的方式来根据最新状态设置和改变css；
- 等等...

Vue在CSS上虽然不能称之为完美，但是已经足够简洁、自然、方便了，至少统一的样式风格不会出现多个开发人员、多个项目采用不一样的样式风格。<br />相比而言，React官方并没有给出在React中统一的样式风格：

- 由此，从普通的css，到css modules，再到css in js，有几十种不同的解决方案，上百个不同的库；
- 大家一致在寻找最好的或者说最适合自己的CSS方案，但是到目前为止也没有统一的方案；

目前普遍有四种解决方案：

- 方案一：内联样式的写法；
- 方案二：普通的css写法；
- 方案三：css modules；
- 方案四：css in js（styled-components）；
<a name="poP4B"></a>
### 2. 普通的解决方案
<a name="nfn6p"></a>
#### 1. 内联样式
内联样式是官方推荐的一种css样式的写法：

- `style` 接受一个采用小驼峰命名属性的 JavaScript 对象，，而不是 CSS 字符串；
- 并且可以引用state中的状态来设置相关的样式；
```javascript
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      titleColor: "red"
    }
  }
  render() {
    return (
      <div>
        <h2 style={{color: this.state.titleColor, fontSize: "20px"}}>我是App标题</h2>
        <p style={{color: "green", textDecoration: "underline"}}>我是一段文字描述</p>
      </div>
    )
  }
}
```
内联样式的优点:

- 1.内联样式, 样式之间不会有冲突<br />
- 2.可以动态获取当前state中的状态<br />

内联样式的缺点：

- 1.写法上都需要使用驼峰标识<br />
- 2.某些样式没有提示<br />
- 3.大量的样式, 代码混乱<br />
- 4.某些样式无法编写(比如伪类/伪元素)<br />

所以官方依然是希望内联合适和普通的css来结合编写；
<a name="OWHAN"></a>
#### 2. 普通的css
普通的css我们通常会编写到一个单独的文件。<br />App.js中编写React逻辑代码：
```javascript
import React, { PureComponent } from 'react';
import Home from './Home';
import './App.css';
export default class App extends PureComponent {
  render() {
    return (
      <div className="app">
        <h2 className="title">我是App的标题</h2>
        <p className="desc">我是App中的一段文字描述</p>
        <Home/>
      </div>
    )
  }
}
```
App.css中编写React样式代码：
```css
.title {
  color: red;
  font-size: 20px;
}
.desc {
  color: green;
  text-decoration: underline;
}
```
这样的编写方式和普通的网页开发中编写方式是一致的：

- 如果我们按照普通的网页标准去编写，那么也不会有太大的问题；
- 但是组件化开发中我们总是希望组件是一个独立的模块，即便是样式也只是在自己内部生效，不会相互影响；
- 但是普通的css都属于全局的css，样式之间会相互影响；

比如编写Home.js的逻辑代码：
```javascript
import React, { PureComponent } from 'react';
import './Home.css';
export default class Home extends PureComponent {
  render() {
    return (
      <div className="home">
        <h2 className="title">我是Home标题</h2>
        <span className="desc">我是Home中的span段落</span>
      </div>
    )
  }
}
```
又编写了Home.css的样式代码：
```css
.title {
  color: orange;
}
.desc {
  color: purple;
}
```
最终样式之间会相互层叠，只有一个样式会生效；
<a name="VPe4p"></a>
#### 3. css modules
css modules并不是React特有的解决方案，而是所有使用了类似于webpack配置的环境下都可以使用的。<br />但是，如果在其他项目中使用，那么我们需要自己来进行配置，比如配置webpack.config.js中的`modules: true`等。<br />但是React的脚手架已经内置了css modules的配置：

- .css/.less/.scss 等样式文件都修改成 .module.css/.module.less/.module.scss 等；
- 之后就可以引用并且进行使用了；

使用的方式如下：<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1602225135999-a69452fa-7401-401c-99ff-8085b5289fcd.webp#align=left&display=inline&height=465&margin=%5Bobject%20Object%5D&originHeight=465&originWidth=1080&size=0&status=done&style=none&width=1080)css modules用法<br />这种css使用方式最终生成的class名称会全局唯一：<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1602225135996-c8941551-7ec4-4438-8d9f-9fd5c67dd867.webp#align=left&display=inline&height=196&margin=%5Bobject%20Object%5D&originHeight=196&originWidth=670&size=0&status=done&style=none&width=670)生成的代码结构<br />css modules确实解决了局部作用域的问题，也是很多人喜欢在React中使用的一种方案。<br />但是这种方案也有自己的缺陷：

- 引用的类名，不能使用连接符(.home-title)，在JavaScript中是不识别的；
- 所有的className都必须使用`{style.className}` 的形式来编写；
- 不方便动态来修改某些样式，依然需要使用内联样式的方式；

如果你觉得上面的缺陷还算OK，那么你在开发中完全可以选择使用css modules来编写，并且也是在React中很受欢迎的一种方式。
<a name="UL9jf"></a>
## 2. CSS in JS
<a name="ZLGGm"></a>
### 1. 认识CSS in JS
实际上，官方文档也有提到过CSS in JS这种方案：

- “CSS-in-JS” 是指一种模式，其中 CSS 由 JavaScript 生成而不是在外部文件中定义；
- _注意此功能并不是 React 的一部分，而是由第三方库提供。_ React 对样式如何定义并没有明确态度；

在传统的前端开发中，我们通常会将结构（HTML）、样式（CSS）、逻辑（JavaScript）进行分离。

- 但是在前面的学习中，我们就提到过，React的思想中认为逻辑本身和UI是无法分离的，所以才会有了JSX的语法。<br />
- 样式呢？样式也是属于UI的一部分；<br />
- 事实上CSS-in-JS的模式就是一种将样式（CSS）也写入到JavaScript中的方式，并且可以方便的使用JavaScript的状态；<br />
- 所以React有被人称之为 `All in JS`；<br />

当然，这种开发的方式也受到了很多的批评：

- Stop using CSS in JavaScript for web development<br />
- [https://hackernoon.com/stop-using-css-in-javascript-for-web-development-fa32fb873dcc](https://hackernoon.com/stop-using-css-in-javascript-for-web-development-fa32fb873dcc)<br />

批评声音虽然有，但是在我们看来很多优秀的CSS-in-JS的库依然非常强大、方便：

- CSS-in-JS通过JavaScript来为CSS赋予一些能力，包括类似于CSS预处理器一样的样式嵌套、函数定义、逻辑复用、动态修改状态等等；
- 依然CSS预处理器也具备某些能力，但是获取动态状态依然是一个不好处理的点；
- 所以，目前可以说CSS-in-JS是React编写CSS最为受欢迎的一种解决方案；

目前比较流行的CSS-in-JS的库有哪些呢？

- styled-components
- emotion
- glamorous

目前可以说styled-components依然是社区最流行的CSS-in-JS库，所以我们以styled-components的讲解为主；<br />安装styled-components：
```javascript
yarn add styled-components
```
<a name="7Jone"></a>
### 2. styled-components
<a name="tEoRd"></a>
#### 1. 标签模板字符串
ES6中增加了`模板字符串`的语法，这个对于很多人来说都会使用。<br />但是模板字符串还有另外一种用法：标签模板字符串（Tagged Template Literals）。<br />我们一起来看一个普通的JavaScript的函数：
```javascript
function foo(...args) {
  console.log(args);
}
foo("Hello World");
```
正常情况下，我们都是通过 `函数名()` 方式来进行调用的，其实函数还有另外一种调用方式：
```javascript
foo`Hello World`; // [["Hello World"]]
```
如果我们在调用的时候插入其他的变量：

- 模板字符串被拆分了；
- 第一个元素是数组，是被模块字符串拆分的字符串组合；
- 后面的元素是一个个模块字符串传入的内容；
```javascript
foo`Hello ${name}`; // [["Hello ", ""], "kobe"];
```
在styled component中，就是通过这种方式来解析模块字符串，最终生成我们想要的样式的
<a name="cI1aK"></a>
#### 2. styled基本使用
styled-components的本质是通过函数的调用，最终创建出一个`组件`：

- 这个组件会被自动添加上一个不重复的class；
- styled-components会给该class添加相关的样式；

比如我们正常开发出来的Home组件是这样的格式：
```html
<div>
  <h2>我是Home标题</h2>
  <ul>
    <li>我是列表1</li>
    <li>我是列表2</li>
    <li>我是列表3</li>
  </ul>
</div>
```
我们希望给外层的div添加一个特殊的class，并且添加相关的样式：<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1602225136052-7fe0bf13-68a0-4981-9da6-7f7ea3fdfd2f.webp#align=left&display=inline&height=565&margin=%5Bobject%20Object%5D&originHeight=565&originWidth=970&size=0&status=done&style=none&width=970)styled-components基本使用<br />另外，它支持类似于CSS预处理器一样的样式嵌套：

- 支持直接子代选择器或后代选择器，并且直接编写样式；
- 可以通过&符号获取当前元素；
- 直接伪类选择器、伪元素等；
```css
const HomeWrapper = styled.div`
  color: purple;
  h2 {
    font-size: 50px;
  }
  ul > li {
    color: orange;
    &.active {
      color: red;
    }
    &:hover {
      background: #aaa;
    }
    &::after {
      content: "abc"
    }
  }
`
```
![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1602225136233-1b400b79-3e09-408e-8e3c-d3bb1f44c627.webp#align=left&display=inline&height=208&margin=%5Bobject%20Object%5D&originHeight=208&originWidth=564&size=0&status=done&style=none&width=564)最终效果如下
<a name="nt401"></a>
#### 3. props、attrs属性
**props可以穿透**<br />定义一个styled组件：
```css
const HYInput = styled.input`
  border-color: red;
  &:focus {
    outline-color: orange;
  }
`
```
使用styled的组件：
```javascript
<HYInput type="password"/>
```
**props可以被传递给styled组件**
```javascript
<HomeWrapper color="blue">
</HomeWrapper>
```
使用时可以获取到传入的color：

- 获取props需要通过${}传入一个插值函数，props会作为该函数的参数；
- 这种方式可以有效的解决动态样式的问题；
```css
const HomeWrapper = styled.div`
  color: ${props => props.color};
}
```
**添加attrs属性**
```css
const HYInput = styled.input.attrs({
  placeholder: "请填写密码",
  paddingLeft: props => props.left || "5px"
})`
  border-color: red;
  padding-left: ${props => props.paddingLeft};
  &:focus {
    outline-color: orange;
  }
`
```
<a name="mzFHu"></a>
#### 4. styled高级特性
**支持样式的继承**<br />编写styled组件
```css
const HYButton = styled.button`
  padding: 8px 30px;
  border-radius: 5px;
`
const HYWarnButton = styled(HYButton)`
  background-color: red;
  color: #fff;
`
const HYPrimaryButton = styled(HYButton)`
  background-color: green;
  color: #fff;
`
```
按钮的使用
```html
<Button>我是普通按钮</Button>
<WarnButton>我是警告按钮</WarnButton>
<PrimaryButton>我是主要按钮</PrimaryButton>
```
**styled设置主题**<br />在全局定制自己的主题，通过Provider进行共享：
```javascript
import { ThemeProvider } from 'styled-components';
<ThemeProvider theme={{color: "red", fontSize: "30px"}}>
  <Home />
  <Profile />
</ThemeProvider>
```
在styled组件中可以获取到主题的内容：
```css
const ProfileWrapper = styled.div`
  color: ${props => props.theme.color};
  font-size: ${props => props.theme.fontSize};
`
```
<a name="5eJzi"></a>
### 3. classnames
**react中添加class**<br />React在JSX给了我们开发者足够多的灵活性，你可以像编写JavaScript代码一样，通过一些逻辑来决定是否添加某些class：
```javascript
import React, { PureComponent } from 'react'
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      isActive: true
    }
  }
  render() {
    const {isActive} = this.state; 
    return (
      <div>
        <h2 className={"title " + (isActive ? "active": "")}>我是标题</h2>
        <h2 className={["title", (isActive ? "active": "")].join(" ")}>我是标题</h2>
      </div>
    )
  }
}
```
这个时候我们可以借助于一个第三方的库：classnames

- 很明显，这是一个用于动态添加classnames的一个库。

我们来使用一下最常见的使用案例：
```javascript
classNames('foo', 'bar'); // => 'foo bar'
classNames('foo', { bar: true }); // => 'foo bar'
classNames({ 'foo-bar': true }); // => 'foo-bar'
classNames({ 'foo-bar': false }); // => ''
classNames({ foo: true }, { bar: true }); // => 'foo bar'
classNames({ foo: true, bar: true }); // => 'foo bar'
// lots of arguments of various types
classNames('foo', { bar: true, duck: false }, 'baz', { quux: true }); // => 'foo bar baz quux'
// other falsy values are just ignored
classNames(null, false, 'bar', undefined, 0, 1, { baz: null }, ''); // => 'bar 1'
```
<a name="kuR3a"></a>
# 十、AntDesign
<a name="fU8tT"></a>
## 1. AntDesign的介绍
`AntDesign` ，简称 `antd` 是基于 Ant Design 设计体系的 React UI 组件库，主要用于研发企业级中后台产品。<br />AntDesign的特点：<br />`全链路开发和设计指的是什么？`

- 全链路这个词16年左右阿里提出的；
- 从`业务战略—用户场景—设计目标—交互体验—用户流程—预期效率`全方面进行分析和考虑；
- 这个主要是产品经理会考虑的一个点；
<a name="vddJV"></a>
# 十一、Axios库
<a name="wSVcA"></a>
## 1. axios库的基本使用
<a name="FlWKz"></a>
### 1.1. 网络请求的选择
目前前端中发送网络请求的方式有很多种：<br />选择一:传统的Ajax是基于XMLHttpReques(XHR)

- 为什么不用它呢?
   - 非常好解释, 配置和调用方式等非常混乱
   - 所以真实开发中很少直接使用, 而是使用jQuery-Ajax

选择二: 在前面的学习中, 我们经常会使用jQuery-Ajax

- 相对于传统的Ajax非常好用.<br />
- 为什么不选择它呢？<br />
   - jQuery整个项目太大，单纯使用ajax却要引入整个JQuery非常的不合理（采取个性化打包的方案又不能享受CDN服务）；
   - 基于原生的XHR开发，XHR本身的架构不清晰，已经有了fetch的替代方案；
   - 尽管JQuery对我们前端的开发工作曾有着深远的影响，但是的确正在退出历史舞台；

选择三: Fetch API

- 选择或者不选择它?
   - Fetch是AJAX的替换方案，基于Promise设计，很好的进行了关注分离，有很大一批人喜欢使用fetch进行项目开发；
   - 但是Fetch的缺点也很明显，首先需要明确的是Fetch是一个 low-level（底层）的API，没有帮助你封装好各种各样的功能和实现；
   - 比如发送网络请求需要自己来配置Header的Content-Type，不会默认携带cookie等；
   - 比如错误处理相对麻烦（只有网络错误才会reject，HTTP状态码404或者500不会被标记为reject）；
   - 比如不支持取消一个请求，不能查看一个请求的进度等等；
   - MDN Fetch学习地址：[https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch](https://developer.mozilla.org/zh-CN/docs/Web/API/Fetch_API/Using_Fetch)

选择四：axios

- axios: ajax i/o system.<br />
- axios是目前前端使用非常广泛的网络请求库，包括Vue作者也是推荐在vue中使用axios；<br />
- 主要特点包括：<br />
   - 在浏览器中发送 XMLHttpRequests 请求；
   - 在 node.js 中发送 http请求；
   - 支持 Promise API；
   - 拦截请求和响应；
   - 转换请求和响应数据；
   - 等等；
<a name="cIdH1"></a>
### 1.2. axios的基本使用
支持多种请求方式:

- paxios(config)<br />
- axios.request(config)<br />
- axios.get(url[, config])<br />
- axios.delete(url[, config])<br />
- axios.head(url[, config])<br />
- axios.post(url[, data[, config]])<br />
- axios.put(url[, data[, config]])<br />
- axios.patch(url[, data[, config]])<br />

**注意：下面的测试我都会使用httpbin.org这个网站来测试，是我个人非常喜欢的一个网站；**<br />我们来发送一个get请求：
```javascript
// 1.发送一个get请求
    axios({
      method: "get",
      url: "https:httpbin.org/get",
      params: {
        name: "coderwhy",
        age: 18
      }
    }).then(res => {
      console.log("请求结果:", res);
    }).catch(err => {
      console.log("错误信息:", err);
    });
```
你也可以直接发送get，那么就不需要传入method（当然不传入默认也是get请求）
```javascript
axios.get("https://httpbin.org/get", {
      params: {
        name: "kobe",
        age: 40
      }
    }).then(res => {
      console.log("请求结果:", res);
    }).catch(err => {
      console.log("错误信息:", err);
    });
```
当然，你也可以使用await、async在componentDidMount中发送网络请求：
```javascript
async componentDidMount() {
    const result = await axios.get("https://httpbin.org/get", {
      params: {
        name: "kobe",
        age: 40
      }
    })
    console.log(result);
  }
```
那么，有错误的时候，await中如何处理呢？使用try-catch来处理错误信息
```javascript
async componentDidMount() {
    try {
      const result = await axios.get("https://httpbin.org/get", {
        params: {
          name: "kobe",
          age: 40
        }
      })
      console.log(result);
    } catch(err) {
      console.log(err);
    }
  }
```
发送多个并发的请求：
```javascript
const request1 = axios.get("https://httpbin.org/get", {
      params: {name: "why", age: 18}
    });
    const request2 = axios.post("https://httpbin.org/post", {
      name: "kobe",
      age: 40
    })
    axios.all([request1, request2]).then(([res1, res2]) => {
      console.log(res1, res2);
    }).catch(err => {
      console.log(err);
    })
```
**选读：axios(config)和axios.get()或axios.post有上什么区别呢？**<br />查看源码就会发现，`axios.get()或axios.post`本质上最终都是在调用axios的request<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1603344156847-c091648c-6134-477c-891d-302314a6db72.webp#align=left&display=inline&height=350&margin=%5Bobject%20Object%5D&originHeight=575&originWidth=1080&size=0&status=done&style=none&width=657)在Axios的原型上添加各种请求方法<br />本质上都是request请求：<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1603344156874-c9804e15-c0fa-49f0-acdf-a1e180cac32d.webp#align=left&display=inline&height=350&margin=%5Bobject%20Object%5D&originHeight=575&originWidth=1080&size=0&status=done&style=none&width=657)本质都是request请求
<a name="glzc7"></a>
### 1.3. axios的配置信息
<a name="JqnQM"></a>
#### 1.3.1. 请求配置选项
下面是创建请求时可以用的配置选项：

- 只有URL是必传的；
- 如果没有指定method，请求将默认使用`get`请求；
```javascript
{
   // `url` 是用于请求的服务器 URL
  url: '/user',
  // `method` 是创建请求时使用的方法
  method: 'get', // default
  // `baseURL` 将自动加在 `url` 前面，除非 `url` 是一个绝对 URL。
  // 它可以通过设置一个 `baseURL` 便于为 axios 实例的方法传递相对 URL
  baseURL: 'https://some-domain.com/api/',
  // `transformRequest` 允许在向服务器发送前，修改请求数据
  // 只能用在 'PUT', 'POST' 和 'PATCH' 这几个请求方法
  // 后面数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
  transformRequest: [function (data, headers) {
    // 对 data 进行任意转换处理
    return data;
  }],
  // `transformResponse` 在传递给 then/catch 前，允许修改响应数据
  transformResponse: [function (data) {
    // 对 data 进行任意转换处理
    return data;
  }],
  // `headers` 是即将被发送的自定义请求头
  headers: {'X-Requested-With': 'XMLHttpRequest'},
  // `params` 是即将与请求一起发送的 URL 参数
  // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
  params: {
    ID: 12345
  },
   // `paramsSerializer` 是一个负责 `params` 序列化的函数
  // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
  paramsSerializer: function(params) {
    return Qs.stringify(params, {arrayFormat: 'brackets'})
  },
  // `data` 是作为请求主体被发送的数据
  // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
  // 在没有设置 `transformRequest` 时，必须是以下类型之一：
  // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
  // - 浏览器专属：FormData, File, Blob
  // - Node 专属：Stream
  data: {
    firstName: 'Fred'
  },
  // `timeout` 指定请求超时的毫秒数(0 表示无超时时间)
  // 如果请求话费了超过 `timeout` 的时间，请求将被中断
  timeout: 1000,
   // `withCredentials` 表示跨域请求时是否需要使用凭证
  withCredentials: false, // default
  // `adapter` 允许自定义处理请求，以使测试更轻松
  // 返回一个 promise 并应用一个有效的响应 (查阅 [response docs](#response-api)).
  adapter: function (config) {
    /* ... */
  },
 // `auth` 表示应该使用 HTTP 基础验证，并提供凭据
  // 这将设置一个 `Authorization` 头，覆写掉现有的任意使用 `headers` 设置的自定义 `Authorization`头
  auth: {
    username: 'janedoe',
    password: 's00pers3cret'
  },
   // `responseType` 表示服务器响应的数据类型，可以是 'arraybuffer', 'blob', 'document', 'json', 'text', 'stream'
  responseType: 'json', // default
  // `responseEncoding` indicates encoding to use for decoding responses
  // Note: Ignored for `responseType` of 'stream' or client-side requests
  responseEncoding: 'utf8', // default
   // `xsrfCookieName` 是用作 xsrf token 的值的cookie的名称
  xsrfCookieName: 'XSRF-TOKEN', // default
  // `xsrfHeaderName` is the name of the http header that carries the xsrf token value
  xsrfHeaderName: 'X-XSRF-TOKEN', // default
   // `onUploadProgress` 允许为上传处理进度事件
  onUploadProgress: function (progressEvent) {
    // Do whatever you want with the native progress event
  },
  // `onDownloadProgress` 允许为下载处理进度事件
  onDownloadProgress: function (progressEvent) {
    // 对原生进度事件的处理
  },
   // `maxContentLength` 定义允许的响应内容的最大尺寸
  maxContentLength: 2000,
  // `validateStatus` 定义对于给定的HTTP 响应状态码是 resolve 或 reject  promise 。如果 `validateStatus` 返回 `true` (或者设置为 `null` 或 `undefined`)，promise 将被 resolve; 否则，promise 将被 rejecte
  validateStatus: function (status) {
    return status >= 200 && status < 300; // default
  },
  // `maxRedirects` 定义在 node.js 中 follow 的最大重定向数目
  // 如果设置为0，将不会 follow 任何重定向
  maxRedirects: 5, // default
  // `socketPath` defines a UNIX Socket to be used in node.js.
  // e.g. '/var/run/docker.sock' to send requests to the docker daemon.
  // Only either `socketPath` or `proxy` can be specified.
  // If both are specified, `socketPath` is used.
  socketPath: null, // default
  // `httpAgent` 和 `httpsAgent` 分别在 node.js 中用于定义在执行 http 和 https 时使用的自定义代理。允许像这样配置选项：
  // `keepAlive` 默认没有启用
  httpAgent: new http.Agent({ keepAlive: true }),
  httpsAgent: new https.Agent({ keepAlive: true }),
  // 'proxy' 定义代理服务器的主机名称和端口
  // `auth` 表示 HTTP 基础验证应当用于连接代理，并提供凭据
  // 这将会设置一个 `Proxy-Authorization` 头，覆写掉已有的通过使用 `header` 设置的自定义 `Proxy-Authorization` 头。
  proxy: {
    host: '127.0.0.1',
    port: 9000,
    auth: {
      username: 'mikeymike',
      password: 'rapunz3l'
    }
  },
  // `cancelToken` 指定用于取消请求的 cancel token
  // （查看后面的 Cancellation 这节了解更多）
  cancelToken: new CancelToken(function (cancel) {
  })
}
```
<a name="rhlGJ"></a>
#### 1.3.2. 响应结构信息
某个请求的响应包含以下信息：
```javascript
{
  // `data` 由服务器提供的响应
  data: {},
  // `status` 来自服务器响应的 HTTP 状态码
  status: 200,
  // `statusText` 来自服务器响应的 HTTP 状态信息
  statusText: 'OK',
  // `headers` 服务器响应的头
  headers: {},
   // `config` 是为请求提供的配置信息
  config: {},
 // 'request'
  // `request` is the request that generated this response
  // It is the last ClientRequest instance in node.js (in redirects)
  // and an XMLHttpRequest instance the browser
  request: {}
}
```
<a name="hAWdB"></a>
#### 1.3.3. 默认配置信息
你可以指定将被用在各个请求的配置默认值：<br />**全局的axios默认配置：**
```javascript
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```
**自定义实例默认配置：**
```javascript
const instance = axios.create({
  baseURL: 'https://api.example.com'
});
// Alter defaults after instance has been created
instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;
```
配置信息的查找顺序如下：

- 优先是请求的config参数配置；
- 其次是实例的default中的配置；
- 最后是创建实例时的配置；
<a name="BAc5S"></a>
### 1.4. axios的拦截器
axios库有一个非常好用的特性是可以添加拦截器：

- 请求拦截器：在发送请求时，请求被拦截；
   - 发送网络请求时，在页面中添加一个loading组件作为动画；
   - 某些网络请求要求用户必须登录，可以在请求中判断是否携带了token，没有携带token直接跳转到login页面；
   - 对某些请求参数进行序列化；
- 响应拦截器：在响应结果中，结果被拦截；
   - 响应拦截中可以对结果进行二次处理（比如服务器真正返回的数据其实是在response的data中）；
   - 对于错误信息进行判断，根据不同的状态进行不同的处理；
```javascript
axios.interceptors.request.use(config => {
  // 1.发送网络请求时，在页面中添加一个loading组件作为动画；
  // 2.某些网络请求要求用户必须登录，可以在请求中判断是否携带了token，没有携带token直接跳转到login页面；
  // 3.对某些请求参数进行序列化；
  return config;
}, err => {
  return err;
})
axios.interceptors.response.use(response => {
  return response.data;
}, err => {
  if (err && err.response) {
    switch (err.response.status) {
      case 400:
        err.message = "请求错误";
        break;
      case 401:
        err.message = "未授权访问";
        break;
    }
  }
  return err;
})
```
<a name="ug4UA"></a>
## 二. axios库的二次封装
<a name="xv6OU"></a>
### 2.1. 为什么要封装
为什么我们要对axios进行二次封装呢？

- 默认情况下我们是可以直接使用axios来进行开发的；
- 但是我们考虑一个问题，假如有100多处中都直接依赖axios，突然间有一天axios出现了重大bug，并且该库已经不再维护，这个时候你如何处理呢？
- 大多数情况下我们会寻找一个新的网络请求库或者自己进行二次封装；
- 但是有100多处都依赖了axios，方便我们进行修改吗？我们所有依赖axios库的地方都需要进行修改；

![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1603344156863-f55cb031-92f8-448d-bb5e-d2775f3c9b15.webp#align=left&display=inline&height=377&margin=%5Bobject%20Object%5D&originHeight=520&originWidth=906&size=0&status=done&style=none&width=657)直接依赖axios<br />如果是自己进行了二次封装，并且暴露一套自己的API：<br />![](https://cdn.nlark.com/yuque/0/2020/webp/1575183/1603344156927-0f9caa92-29ae-454c-8a2b-c615004e777b.webp#align=left&display=inline&height=454&margin=%5Bobject%20Object%5D&originHeight=637&originWidth=922&size=0&status=done&style=none&width=657)自己进行二次封装
<a name="vOk63"></a>
### 2.2. axios二次封装
创建一个service文件夹（其他名字都可以），用于存放所有的网络请求相关的内容。<br />创建文件config.js，用于存放一些配置信息：
```javascript
export const TIMEOUT = 5000;
const devBaseURL = "https://httpbin.org";
const proBaseURL = "https://production.org";
console.log(process.env.NODE_ENV);
export const baseURL = process.env.NODE_ENV === 'development' ? devBaseURL: proBaseURL;
```
创建request.js，用于封装请求对象：
```javascript
import axios from 'axios';
import {
  TIMEOUT,
  baseURL
 } from "./config";
const instance = axios.create({
  timeout: TIMEOUT,
  baseURL: baseURL
})
axios.interceptors.request.use(config => {
  // 1.发送网络请求时，在页面中添加一个loading组件作为动画；
  // 2.某些网络请求要求用户必须登录，可以在请求中判断是否携带了token，没有携带token直接跳转到login页面；
  // 3.对某些请求参数进行序列化；
  return config;
}, err => {
  return err;
})
instance.interceptors.response.use(response => {
  return response.data;
}, err => {
  if (err && err.response) {
    switch (err.response.status) {
      case 400:
        err.message = "请求错误";
        break;
      case 401:
        err.message = "未授权访问";
        break;
    }
  }
  return err;
})
export default instance;
```
使用测试：
```javascript
request({
  url: "/get",
  params: {
    name: "why",
    age: 18
  }
}).then(console.log).catch(console.error);
request({
  url: "/post",
  method: "post",
  data: {
    name: "kobe",
    age: 40
  }
}).then(console.log).catch(console.error);
```
<a name="5rmnV"></a>
# 十二、React过渡动画
<a name="Ge1bk"></a>
## 一. react-transition-group介绍
React曾为开发者提供过动画插件 `react-addons-css-transition-group`，后由社区维护，形成了现在的 `react-transition-group`。<br />这个库可以帮助我们方便的实现组件的 `入场` 和 `离场` 动画，使用时需要进行额外的安装：
```javascript
# npm
npm install react-transition-group --save
# yarn
yarn add react-transition-group
```
react-transition-group本身非常小，不会为我们应用程序增加过多的负担。<br />react-transition-group主要包含四个组件：

- Transition
   - 该组件是一个和平台无关的组件（不一定要结合CSS）；
   - 在前端开发中，我们一般是结合CSS来完成样式，所以比较常用的是CSSTransition；
- CSSTransition
   - 在前端开发中，通常使用CSSTransition来完成过渡动画效果
- SwitchTransition
   - 两个组件显示和隐藏切换时，使用该组件
- TransitionGroup
   - 将多个动画组件包裹在其中，一般用于列表中元素的动画；
<a name="vsyub"></a>
## 二. react-transition-group使用
<a name="DZOiZ"></a>
### 2.1. CSSTransition
CSSTransition是基于Transition组件构建的：

- CSSTransition执行过程中，有三个状态：appear、enter、exit；
- 它们有三种状态，需要定义对应的CSS样式：
   - 第一类，开始状态：对于的类是-appear、-enter、exit；
   - 第二类：执行动画：对应的类是-appear-active、-enter-active、-exit-active；
   - 第三类：执行结束：对应的类是-appear-done、-enter-done、-exit-done；

CSSTransition常见对应的属性：

- in：触发进入或者退出状态
   - 如果添加了`unmountOnExit={true}`，那么该组件会在执行退出动画结束后被移除掉；
   - 当in为true时，触发进入状态，会添加-enter、-enter-acitve的class开始执行动画，当动画执行结束后，会移除两个class，并且添加-enter-done的class；
   - 当in为false时，触发退出状态，会添加-exit、-exit-active的class开始执行动画，当动画执行结束后，会移除两个class，并且添加-enter-done的class；
- classNames：动画class的名称
   - 决定了在编写css时，对应的class名称：比如card-enter、card-enter-active、card-enter-done；
- timeout：
   - 过渡动画的时间
- appear：
   - 是否在初次进入添加动画（需要和in同时为true）
- 其他属性可以参考官网来学习：
   - [https://reactcommunity.org/react-transition-group/transition](https://reactcommunity.org/react-transition-group/transition)

CSSTransition对应的钩子函数：主要为了检测动画的执行过程，来完成一些JavaScript的操作

- onEnter：在进入动画之前被触发；
- onEntering：在应用进入动画时被触发；
- onEntered：在应用进入动画结束后被触发；
```javascript
import './App.css'
import { CSSTransition } from 'react-transition-group';
import { Card, Avatar, Button } from 'antd';
import { EditOutlined, EllipsisOutlined, SettingOutlined } from '@ant-design/icons';
const { Meta } = Card;
export default class App extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      isShowCard: true
    }
  }
  render() {
    return (
      <div>
        <Button type="primary" onClick={e => this.setState({isShowCard: !this.state.isShowCard})}>显示/隐藏</Button>
        <CSSTransition in={this.state.isShowCard}
                       classNames="card"
                       timeout={1000}
                       unmountOnExit={true}
                       onEnter={el => console.log("进入动画前")}
                       onEntering={el => console.log("进入动画")}
                       onEntered={el => console.log("进入动画后")}
                       onExit={el => console.log("退出动画前")}
                       onExiting={el => console.log("退出动画")}
                       onExited={el => console.log("退出动画后")}
                      >
          <Card
            style={{ width: 300 }}
            cover={
              <img
                alt="example"
                src="https://gw.alipayobjects.com/zos/rmsportal/JiqGstEfoWAOHiTxclqi.png"
              />
            }
            actions={[
              <SettingOutlined key="setting" />,
              <EditOutlined key="edit" />,
              <EllipsisOutlined key="ellipsis" />,
            ]}
          >
            <Meta
              avatar={<Avatar src="https://zos.alipayobjects.com/rmsportal/ODTLcjxAfvqbxHnVXCYX.png" />}
              title="Card title"
              description="This is the description"
            />
          </Card>
        </CSSTransition>
      </div>
    )
  }
}
```
对应的css样式如下：
```css
.card-enter, .card-appear {
  opacity: 0;
  transform: scale(.8);
}
.card-enter-active, .card-appear-active {
  opacity: 1;
  transform: scale(1);
  transition: opacity 300ms, transform 300ms;
}
.card-exit {
  opacity: 1;
}
.card-exit-active {
  opacity: 0;
  transform: scale(.8);
  transition: opacity 300ms, transform 300ms;
}
```
<a name="EsNqc"></a>
### 2.2. SwitchTransition
SwitchTransition可以完成两个组件之间切换的炫酷动画：

- 比如我们有一个按钮需要在on和off之间切换，我们希望看到on先从左侧退出，off再从右侧进入；
- 这个动画在vue中被称之为 vue transition modes；
- react-transition-group中使用SwitchTransition来实现该动画；

SwitchTransition中主要有一个属性：mode，有两个值

- in-out：表示新组件先进入，旧组件再移除；
- out-in：表示就组件先移除，新组建再进入；

如何使用SwitchTransition呢？

- SwitchTransition组件里面要有CSSTransition或者Transition组件，不能直接包裹你想要切换的组件；
- SwitchTransition里面的CSSTransition或Transition组件不再像以前那样接受in属性来判断元素是何种状态，取而代之的是key属性；

我们来演练一个按钮的入场和出场效果：
```javascript
import { SwitchTransition, CSSTransition } from "react-transition-group";
export default class SwitchAnimation extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      isOn: true
    }
  }
  render() {
    const {isOn} = this.state;
    return (
      <SwitchTransition mode="out-in">
        <CSSTransition classNames="btn"
                       timeout={500}
                       key={isOn ? "on" : "off"}>
          {
          <button onClick={this.btnClick.bind(this)}>
            {isOn ? "on": "off"}
          </button>
        }
        </CSSTransition>
      </SwitchTransition>
    )
  }
  btnClick() {
    this.setState({isOn: !this.state.isOn})
  }
}
```
对应的css代码：
```css
.btn-enter {
  transform: translate(100%, 0);
  opacity: 0;
}
.btn-enter-active {
  transform: translate(0, 0);
  opacity: 1;
  transition: all 500ms;
}
.btn-exit {
  transform: translate(0, 0);
  opacity: 1;
}
.btn-exit-active {
  transform: translate(-100%, 0);
  opacity: 0;
  transition: all 500ms;
}
```
<a name="PhrJN"></a>
### 2.3. TransitionGroup
当我们有一组动画时，需要将这些CSSTransition放入到一个TransitionGroup中来完成动画：
```javascript
import React, { PureComponent } from 'react'
import { CSSTransition, TransitionGroup } from 'react-transition-group';
export default class GroupAnimation extends PureComponent {
  constructor(props) {
    super(props);
    this.state = {
      friends: []
    }
  }
  render() {
    return (
      <div>
        <TransitionGroup>
          {
            this.state.friends.map((item, index) => {
              return (
                <CSSTransition classNames="friend" timeout={300} key={index}>
                  <div>{item}</div>
                </CSSTransition>
              )
            })
          }
        </TransitionGroup>
        <button onClick={e => this.addFriend()}>+friend</button>
      </div>
    )
  }
  addFriend() {
    this.setState({
      friends: [...this.state.friends, "coderwhy"]
    })
  }
}
```
