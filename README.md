# 代码风格

### 1、视觉清晰度规则

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
