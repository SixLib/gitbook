# 特点

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

* [特点](#特点)
	* [异步 I/O](#异步-io)
		* [描述](#描述)
		* [为什么要异步I/O](#为什么要异步io)
			* [用户体验](#用户体验)
	* [事件与回调函数](#事件与回调函数)
	* [单线程](#单线程)
	* [跨平台](#跨平台)

<!-- /code_chunk_output -->

## 异步 I/O

### 描述

在nodejs中，绝大多数的操作都是以异步的方式进行调用。 **每个调用之间不用等待之前的I/O调用结束。** 在编程模型上可以极大的提高效率。下面的两个文件读取任务的耗时取决于最慢的那个文件读取的耗时：

``` node
fs.readFile('/path1',function(err,file)
{
    console.log('读取文件1完成')
})
fs.readFile('/path2',function(err,file)
{
    console.log('读取文件2完成')
})
```

而对于同步I/O而言，它们的耗时是两个任务的耗时之和。这里异步带来的优势是显而易见的。

### 为什么要异步I/O

关于异步I/O为何在Node中如此的重要，这与Node是面向网络而设计不无关系。
具体到实处，可以从**用户体验**和**资源分配**这两个方面说起。

#### 用户体验

因为浏览器中JavaScript在单线程上执行，而且它还与UI渲染公用一个线程。这意味着JavaScript在执行的时候UI渲染和相应是处于停滞状态的。

``` text
如果脚本的执行时间超过100ms,用户就会感到页面卡顿，以为页面停滞相应。 —— 《高新能JavaScript》
```

采用异步I/O时，JavaScript和UI的执行都不会处于等待状态，可以继续响应用户的相互行为，给用户一个鲜活的页面。

## 事件与回调函数

nodejs 将前端浏览器中应用广泛的且成熟的事件引入后端，配合异步I/O，将事件点暴露给业务逻辑。
下面的例子展示的是Ajax异步提交的服务器端处理过程。Node创建一个Web服务器，并侦听8080端口。对于服务器，我们为其绑定了request事件，对于请求对象，我们为其绑定了data事件和end事件：

``` node
var http = require('http')
var querystring = require('querystring')

//侦听服务器的request事件
http.createServer(function(req, res)
{
    var postData = ''
    req.setEncoding('utf8')
    //侦听请求的data事件
    req.on('data',function(chunk)
    {
        postData += chunk
    })

    //侦听请求的end事件
    req.on('end', function()
    {
        res.end(postData)
    })
}).listen(8080)
console.log('服务器启动完成')
```

事件的编程方式具有轻量级、松耦合、只关注事物点灯优势，但是在多个异步任务的场景下，事件与事件之间各自独立，如何写作是一个问题。

Node除了异步和事件外，回调函数是一个大特色，也是最好的接收异步调用返回数据的方式。

## 单线程

Node保持了javascript在浏览器中单线程的特点。而且在Node中，Javascript与其余线程是无法共享热河状态的。**单线程最大的好处是不用想像多线程编程那样处处在意状态的同步问题，这里没有死锁的存在，也没有线程上下文交换所带来的性能上的开销。**
单线程也有它自身的弱点：

- 无法理由多核CPU

- 错误会引起整个应有退出，应用的健壮性值得考验

- 大量计算占用CPU导致无法继续调用异步I/O

像浏览器中Javascript与UI共用一个线程一样，JavaScript长时间执行会导致UI的渲染和相应被中断。在Node中，长时间的CPU占用也会导致后续的异步I/O发不出调用，已完成的异步I/O的回调函数也会得不到及时执行。

Node采用了与Web Workers相同的思路来解决单线程中大计算量的问题：**child_process(子进程)**

## 跨平台

起初，Node只可以在Linux平台上运行。随着Node的发展，微软投入了一个团队帮助Node实现Windows平台的兼容。在v0.6.0版本发布时，Node已经能够直接在Windows平台上运行了。

