# javascript 设计模式

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

* [javascript 设计模式](#javascript-设计模式)
	* [构造器模式](#构造器模式)
	* [模块化模式](#模块化模式)

<!-- /code_chunk_output -->

## 构造器模式

``` javascript
var Car = function (model, year, miles) {
    this.model = model;
    this.year = year;
    this.miles = miles;
}
Car.prototype.toString = function() {
    return JSON.stringify(this);
}
var bmw = new Car({
    name: '宝马230'
},
2018, 300);
console.log(bmw.toString());
//输出：{"model":{"name":"宝马230"},"year":2018,"miles":300}
```

## 模块化模式

``` javascript
var myModule = function()
{
return {
    name: 'sixlib',
    config: {
        url: 'sixlib.gitlib.io',
        language: 'zh-cn'
    },
    myMethod: function() {
        console.log(this.name)
    },
    myMethod1: function(config) {
        this.config.language = config.language;
        this.config.url = config.url;
        console.log(JSON.stringify(this.config));
    }
}
}
myModule.myMethod();
//输出： sixlib

myModule.myMethod1({
    url: 'baidu.com',
    language: '中文'
});
//输出：{"url":"baidu.com","language":"中文"}
```