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


否则，如果有时返回值、有时不返回值，会给调试代码带来不便
