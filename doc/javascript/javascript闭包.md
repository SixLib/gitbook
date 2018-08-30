# javascript 闭包

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

* [javascript 闭包](#javascript-闭包)
	* [词法作用域](#词法作用域)
	* [闭包](#闭包)
	* [用闭包模拟私有方法：模块模式(module pattern)](#用闭包模拟私有方法模块模式module-pattern)
	* [在循环中创建一个闭包：*是一个常见的错误*](#在循环中创建一个闭包是一个常见的错误)
	* [性能考量](#性能考量)

<!-- /code_chunk_output -->

## 词法作用域

``` javascript
function init() {
    var name = "sixlib"; // name 是一个被 init 创建的局部变量
    function displayName() { // displayName() 是内部函数,一个闭包
        alert(name); // 使用了父函数中声明的变量
    }
    displayName();
}
init();
```

`displayName()`内的`alert()`显示额父级函数中声明的`name`变量值。

## 闭包

``` javascript
function makeFunc()
{
    var name='sixlib';
    function displayName()
    {
        alert(name);
    }
    return displayName;//displayName()被外部调用
}
var myFunc=makeFunc();//创建displayName()实例引用
myFunc();
```

`myFunc`是执行`makeFunc`时创建的`displayName`函数实例的引用，而`displayName`实例仍可访问其词法作用域中的变量，即可以访问到`name`。由此，当`myFunc`被调用时`name`仍可被访问。

``` javascript
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2));  // 7
console.log(add10(2)); // 12
```

## 用闭包模拟私有方法：模块模式(module pattern)

原生javascript是不支持私有方法的，但我们可以是闭包来模拟私有方法。私有方法不仅有利于限制对代码的访问；还提供了管理全局命名空间的能力，避免变量污染。这种方法也被称为[模块模式(module pattern)](http://wiki.jikexueyuan.com/project/javascript-design-patterns/modular-model.html)

``` javascript
/**
 * Counter:匿名函数体
 * 返回一个对象
 */
var Counter=(function()
{
    /**
     * privateCounter 私有对象
     */
    var privateCounter=0;
    /**
     * changeBy(val)私有函数
     * val 传入变量
     */
    function changeBy(val)
    {
        privateCounter+=val;//privateCounter与val求和
    }
    /**
     * 返回对象
     * increment 计数器函数
     * decrement 计数器函数
     * value 技术结果函数
     */
    return {
        increment:function()
        {
            changeBy(1);
            return this;//计算后返回自身
        },
        decrement:function()
        {
            changeBy(-1);
            return this;//计算后返回自身
        },
        value:function()
        {
            return privateCounter;
        }
    }
})()
console.log(Counter.value());/* 输出 0 */

Counter.increment().increment();
console.log(Counter.value());/* 输出 2 */

Counter.decrement()
console.log(Counter.value());/* 输出 1 */

```

以上代码创建了一个立即执行匿名函数体`Counter`，该作用域中包含两个私有项：`privateCounter`变量和`changeBy`函数，两项都无法z爱匿名函数外直接访问,必须通过匿名函数返回三个公共函数访问。

三个公共函数是共享一个环境的闭包.

``` javascript
var Counter=(function()
{
    var privateCounter=0;
    function changeBy(val)
    {
        privateCounter+=val;
    }
    return {
        increment:function()
        {
            changeBy(1);
            return this;
        },
        decrement:function()
        {
            changeBy(-1);
            return this;
        },
        value:function()
        {
            return privateCounter;
        }
    }
});

var Counter1=Counter();
var Counter2=Counter();
Counter1.increment();
console.log(Counter1.value());
console.log(Counter2.value());

```

## 在循环中创建一个闭包：*是一个常见的错误*

## 性能考量

如果不是某些特定任务需要闭包，在其他函数中创建函数是不明智的，这意味着不再需要额外的闭包。

``` javascript
function MyObject(name, message) {
  this.name = name.toString();
  this.message = message.toString();
  this.getName = function() {
    return this.name;
  };

  this.getMessage = function() {
    return this.message;
  };
}
```

如上代码没有用到闭包的好处，可以修改成如下：

``` javascript
function MyObject(name, message) {
  this.name = name.toString();
  this.message = message.toString();
}
MyObject.prototype{
  getName : function() {
    return this.name;
  },
  getMessage : function() {
    return this.message;
  }
}
```

但是不建议重新定义原型；如下

``` javascript
function MyObject(name, message) {
  this.name = name.toString();
  this.message = message.toString();
}
MyObject.prototype.getName = function() {
  return this.name;
};

MyObject.prototype.getMessage = function() {
  return this.message;
}

```
