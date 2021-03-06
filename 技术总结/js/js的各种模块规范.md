# js的各种模块化规范
> 2018.8.12
## 前言
    js有很多模块规范现在主要接触的是CommonJS和ES6的模块规范，但是对于模块的最重要的区别还是有点没懂，现在好好研究一下

## 正文
### 一、主要的模块规范
#### 1.CommonJs

CommonJs的模块规范主要是应用于nodeJs，它是以同步方式加载模块的，由于在服务端模块文件都储存于磁盘，读取速度回很快，所以不会造成问题，但是在浏览器端的话要通过网络请求去取模块文件，这样在加载模块文件那块就会导致网页假死，所以一般不在浏览器端使用该规范。

使用方法：CommonJs的模块有这module（代表整个模块对象）、exports（moudule.exports = exports）、require、global者几个关键字，通常使用时通过exports来定义导出的接口，最后通过require引入即可。

#### 2.ES6

由于有很多模块规范，没有统一的标准，在ES6的时候终于完成对模块语法层的实现，ES6的模块可以在浏览器端和服务端统一使用，而ES6的模块不是对象，它通过import命令在编译时引入指定的模块代码，而不是通过运行时加载。

使用方式：通过export定义导出的接口，因为使用import引入的时候需要知道引入接口的名称，这样可以使用export default命令导出默认接口来解决。

#### 3.AMD和CMD
在ES6的模块规范还没有出来的时候，浏览器的模块规范主要是由AMD和CMD进行定义的，他们都是支持异步加载模块，通过
这样就解决了页面假死的情况，两则最主要的区别是：1）AMD是requireJs的实现、CMD是seaJs的实现；2）AMD推崇依赖前置、提前执行，而CMD推崇依赖后置、延迟执行。

### 二、CommonJs和ES6模块规范的最主要区别

- CommonJs是运行时加载：CommonJs的模块是对象，所以只要运行时才能获取对象的属性和方法，这样导致CommonJs只能是在运行时使用。
- ES6模块是静态加载或者编译时加载：ES6的模块通过exports指定输出的代码，然后import引入，故在编译时就已经完成模块的加载，效率会高很多，且使得静态分析成为可能；但是因为模块不是对象，模块就不能引用自身。

## 参考文章
- [ECMAScript 6 入门](http://es6.ruanyifeng.com/)
- [前端模块化：CommonJS,AMD,CMD,ES6](https://juejin.im/post/5aaa37c8f265da23945f365c)
- [前端模块化，AMD与CMD的区别](https://juejin.im/post/5a422b036fb9a045211ef789)
