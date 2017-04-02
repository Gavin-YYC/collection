# 代码风格

总结常用的代码风格，统一团队风格。我们常说风格，那么风格有什么作用？

* 一致性
* 表达能力
* 简介
* 约束性

在JavaScript专家编程中，作者将风格分为两部分：

* 视觉清晰度规则
* 计算有效性规则

### 1、视觉清晰度规则

#### 1、命名约定

#### 2、常量与变量

#### 3、空白行

#### 4、逗号

#### 5、分号

#### 6、空格

空格不应该出现在空函数或空对象字面量中：

    // bad
    var foo = { };
    var arr = [ ];

    // good
    var foo = {};
    var arr = [];

#### 7、方括号和大括号

    // bad
    if ( hidden )
    {
      // ...
    }

    // good
    if ( hidden ) {
      // ...
    }

可读性胜过简洁，让代码压缩工具来解决使代码变小的问题：

    // bad
    if ( false ) return;

    // good
    if ( false ) {
      return;
    }

结合空格可以让代码阅读起来更舒适：

    // bad 没有空格
    if(true){
      //...
    }

    // good 一个空格
    if ( true ) {
      // ...
    }

    // bad 参数间没有空格
    if (a,b,c) {}

    // good 参数间存在空格
    if (a, b, c) {}

#### 8、字符串

为了一致性，字符串应当使用单引号创建，这还能区分使用双引号的对象字面量和JSON。

    // bad
    var foo = "bar";

    // good
    var foo ='bar';

#### 9、函数



#### 10、注释

注释不应该放到语句的后面，应该放到语句上面：

    // bad
    var findfoo = doSth( isFoo ) // 注释不要写在这里

    // god
    // 注释放到这里
    var findfoo = doSth( isFoo )

注释应当谨慎使用，过多注释实际上说明代码表达的意义不清晰。

注释应当始终表达一个完整的思想。

### 2、计算有效性规则

#### 1、使用全等与全不等

  使用`===`代替`==`，使用`!==`代替`!=`。

    if ( a === b ) {
      // then
    }

#### 2、显式类型转换

    var num = '1';

    // bad
    num = +num;

    // good
    num = Number( num );

#### 3、函数返回值

* 要么函数永远都返回值
* 要么函数永远都不返回值

      function doSth () {
        if ( true ) {
          return something;
        } else {
          return something;
        }
      }

#### 4、不用的变量设置为null

当删除一个变量时，将其设置为null，而不是调用delete或将其设置为undefined：

    // bad case
    this.unwanted = undefined;

    // also bad case
    delete this.unwanted

    // good
    this.unwanted = null;

#### 5、函数表达式

相比函数声明，函数表达式有更多的写法：

    // 匿名函数
    var fn = function () {}

    // 具名函数
    var fn = function add () {}

    // 立即执行函数
    (function main() {})();

相比函数声明，函数表达式是首选，因为在旧的浏览器中存在某些bug。

请不要在块语句中使用函数声明，它们不是ECMAScript中的一部分，使用函数表达式来代替：

    // bad
    if ( true ) {
      function bounce() {}
      return bounce();
    }

    // good
    if ( true ) {
      var bounce = function () {
        // 执行语句
      }
    }

#### 6、对象

首先对象的键不要使用保留字，容易产生意想不到的结果：

    // bad
    var obj = { class: 'name' }

    // good
    var obj = { klass: 'name' }

使用字面量来创建对象或数组：

    // ok
    var obj = new Object();
    obj.age = 18;
    obj.name = 'Tom';

    // better
    var obj = {
      age: 18,
      name: 'Tom'
    }

    // ok
    var arr = new Array();

    // better
    var arr = []

#### 7、运行上下文和作用域

如果可能的话，把你的代码包裹在立即调用函数表达式内（IIFE）。它能隔离代码免受他人的污染，并使其更容易抽象成可重用的模块：

    // good
    ;(function ( window, document, undefined ) {
      // My Awesome Library
    })(this, document);

为了防止代码被破坏，在声明严格模式的时候，应该包裹在IIFE模块内或函数中：

    // good
    ;(function () {
      "use strict";
      var fn = function () {}
    })()

设计与持续时间无关的执行代码：

    // bad 因为这可能超过100ms
    setInterval(function () {
      findfoo();
    }, 100);

    // good 只有在findfoo执行完才调用一次
    ;(function main() {
        findfoo();
        setTimeout( main, 100 );
    })();

#### 8、其他补充

* 抵制eval()的使用，它往往是一个恶意代码执行的注入点
* 抵制with()的使用，它会使代码难以理解
* 保持质朴的原型：切勿改装内置的原型如Array.prototype，因为它会无声无息的破坏别人期望得到的标准代码的行为
* 使你的代码与浏览器无关：通过抽象业务逻辑代码与浏览器代码相互分离
* 串联代码：现代应用中经常将多个JavaScript代码合并为一个压缩的精简文件，你应该确保编程脚本免受上下文或作用域转变带来的影响

#### 9、实施代码风格

* 美化器 [JS Beautify](https://github.com/beautify-web/js-beautify)
* IDE - 项目级别的配置系统 [EditorConfig](http://editorconfig.org/)
* JSHint [JSHint](http://jshint.com/)

## 相关参考：

* 《JavaScript专家编程》
* 《JavaScript语言精粹》
* 《JavaScript高级程序设计第三版》

## 其他风格指南

* [Principles of Writing Consistent, Idiomatic JavaScript](https://github.com/rwaldron/idiomatic.js)
* Google JavaScript风格指南 [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
* Airbnb JavaScript风格指南 [JavaScript Style Guide](https://github.com/airbnb/javascript)
* jQuery 风格指南 [JavaScript Style Guide](http://contribute.jquery.org/style-guide/js/)
