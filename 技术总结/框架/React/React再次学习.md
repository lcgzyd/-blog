# React再次学习
> 2018.09.18

## 前言
    来公司的时候给我了点时间学习React,自己先把官方文档看了一遍，包括redux，很快看完也很快忘掉，有很多特性都忘了，在实际业户操作中自己也就写点小的实例，所以用到的东西应该不多，所以这次想认认真真的学一次！

## 正文
### 一、jsx
#### 1.JSX 防止注入攻击
默认情况下， 在渲染之前, React DOM 会格式化(escapes) JSX中的所有值. 从而保证用户无法注入任何应用之外的代码. 在被渲染之前，所有的数据都被转义成为了字符串处理。 以避免 XSS(跨站脚本) 攻击。
### 二、组件
#### 1.组件定义
从定义上来说， 组件就像JavaScript的函数。组件可以接收任意输入(称为”props”)， 并返回 React 元素，用以描述屏幕显示内容。
#### 2.函数组件和类组件
函数组件更加符合上面给出的定义，而类组件则是可以理解为一种函数组件的语法糖，这使得组件的在声明的时候会更加显而易见，两者最大的区别在于：函数组件是一个展示组件，不会有自己的state(状态)，纯靠props传递数据进行展示，故组件里面不会有复杂的逻辑；类组件则是逻辑组件，因为其有生命周期、state(状态)，故可以处理一些复杂的逻辑，一般用了封装拥有复杂逻辑的组件
注意：
- 组件名称总是以大写字母开始
- 所有 React 组件都必须是纯函数，并禁止修改其自身 props
- 更新state必须要使用setState(),且setState()是异步的
#### 2.组件间传参的方式
- props
- context

### 3.组件的生命周期
react组件的生命周期主要分为三个阶段：初始化阶段、运行阶段和销毁阶段

- （1）初始化阶段：
  - 设置组件默认属性
  - 设置组件初始化状态，主要执行constructor函数
  - componentWillMount: 组件渲染前会触发，此时DOM还没有挂载，不能操作DOM，但是可以进行请求数据
  - render(),组件进行渲染
  - componentDidMount: 组件的DOM结构已经挂载，可以进行DOM操作

- （2）运行阶段
  - componentWillReceiveProps: 父组件传递的Props有更新时之前触发
  - shouldComponentUpdate：当组件接受到新的props或者state更新时触发，首次渲染不会触发，此时可以进行性能优化，return false将不会进行组件的重新渲染过程，return true则会继续就行
  ```javascipt
  shouldComponentUpdate(newProps, newState) {
    if (newProps.number < 5) return true;
    return false
  }
  //该钩子函数可以接收到两个参数，新的属性和状态，返回true/false来控制组件是否需要更新。
  ```
  - componentWillUpdate: 组件更新前触发
  - render(): 组件更新渲染
  - componentDidUpdate:  组件更新后触发，此时的DOM已经更新好，可以进行DOM操作了 

-  (3)销毁阶段
  -componentWillUnmount: 组件卸载前触发

![image]('../../../img/')
### 三、受控组件和不受控组件
#### 1.受控组件
react组件都是通过props和state来保持组件的状态，而组件通过这些状态来进行页面的展现；而一些原生DOM元素会通过用户的输入来进行自身形态的改变，比如input、select元素，结合上面的两点，通过这些标签的value属性来绑定state来到控制显示，再通过onChange事件来完成控制输入，就是所谓的受控组件，就是字面意思，组件的输入输出都会受到控制；这种方式的优点就是可以对用户输入的数据就行控制，缺点就是每个受控组件都要绑定onChange事件，虽然可以通过类似事件代理的机制解决大多数的输入处理，但是随着受控组件数量增加，编写的代码量也会增加很多。
####  2.非受控组件
字面意思理解，输入输出都不会受到控制，比如input的type为file的这个元素，他的value是只可以读，故不能对其的输入输出进行控制，而你要在获取这个元素的状态自由通过ref获取这个元素的引用，然后通过原生的方法去访问这个元素中的内容。有点就是上面非受控组件的缺点，不用写时间处理函数，而缺点就是ref这个特性是官方建议不要使用的，这样会导致组件的耦合，违背了组件化的思想。

  defaultValue可以为非受控组件设置默认值，但保留后续更新不受控制。
### 四、上下文
context上下文，react提供的跨层级组件间数据交流的一个解决方案，使用方法是通过在组件树中使用React.createContext，然后提供默认值和Provider，然后在该组件的后续子孙组件中使用Consumer来进行获取该值（默认是寻找里自身组件最近的祖先组件的提供的Provider的值），我觉得不推荐使用，使用情况只有在项目中没有使用reudx做状态管理的情况下，某个地方迫切需要跨多层级进行数据交流。
### 五、高阶组件
    高阶组件是一个函数，能够接受一个组件并返回一个新的组件。

### 六、插槽
#### 1.片段(fragments)
由于在render()函数中有很多情况是必须要返回只有一个父节点的jsx的表达式，比如:渲染列表的时候;而通过<React.Fragment>这个标签可以让你为你添加一个父节点，而在真正渲染的时候不会出现这个多于的标签，
```javascript
render() {
  return (
    <React.Fragment>
      <ChildA />
      <ChildB />
      <ChildC />
    </React.Fragment>
  );
}
```
## 参考文章
- [React中文官网](http://react.css88.com/docs)
- [图解ES6中的React生命周期](https://juejin.im/post/5a062fb551882535cd4a4ce3)