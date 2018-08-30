

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

* [nodejs 笔记](#nodejs-笔记)
	* [什么是错误优先的回调函数？](#什么是错误优先的回调函数)
	* [如何避免回调地狱？](#如何避免回调地狱)
	* [什么是Promise?](#什么是promise)
	* [用什么工具保证一致的代码风格？为什么要这样？](#用什么工具保证一致的代码风格为什么要这样)
	* [什么是Stub?举例说明](#什么是stub举例说明)
	* [什么是测试金字塔？举例说明](#什么是测试金字塔举例说明)
	* [Cookies如何防范XSS攻击？](#cookies如何防范xss攻击)
	* [如何保证依赖的安全性？](#如何保证依赖的安全性)
	* [附加题](#附加题)
		* [这段代码有什么问题？](#这段代码有什么问题)
		* [这段代码有什么问题？](#这段代码有什么问题-1)
		* [这段代码的输出是什么？](#这段代码的输出是什么)

<!-- /code_chunk_output -->

# nodejs 笔记

## 什么是错误优先的回调函数？

错误优先的回调函数（Error-Frist Callback）用于同步时返回错误和数据，第一个参数错误，并且验证它是否出错；其他参数用于返回数据。

``` node
fs.readfile(filePath, function(err,data){
    if(err){
        //处理错误
        return console.log(err);
    }
    console.log(data)
})
```

## 如何避免回调地狱？

以下方式可以避免回调地狱：

- 模块化：将回调函数转换成独立的函数
- 使用流程控制库，例如[async](https://npm.taobao.org/package/async)
- 使用Promise
- 使用async/await([参考async/await替换Promise的6个理由](https://blog.fundebug.com/2017/04/04/nodejs-async-await/))

## 什么是Promise?

Promise可以帮助我们更好的处理异步操作.下面的实例中，100ms后悔打印result字符串，catch用于错误处理。多个Promise可以连接起来。

``` node
new Promise((resolve, reject) =>
{
    setTimeout(() => {
        resolve('result');
    }, 100)
})
.then(console.log('log'))
.catch(console.error('err')
```

## 用什么工具保证一致的代码风格？为什么要这样？

团队协作时，保证一致的代码风格重要的，这样团队成员才可以更快的修改代码，而不需要每一次去适应新的风格。这些根据可以帮助我们：

- ESlint
- Standard

感兴趣的话，可以参考[Javascript Clean Coding](https://blog.risingstack.com/javascript-clean-coding-best-practices-node-js-at-scale/)

## 什么是Stub?举例说明

Stub用于模拟模块的行为。测试时，Stub可以为函数电泳返回模拟的结果。比如说，当我们写文件时，实际上并不需要咋整去写。

``` node
var fs = require('fs');
var writeFileStub = sinon.stub(fs, 'writeFile', function(path, data, cb)
{
    return cb(null);
});
expect(writeFileStub).to.be.called;
writeFileStub.restore();
```

## 什么是测试金字塔？举例说明

测试金字塔反映了需要写的单元测试、集成测试以及端到端测试的比例：
![image](/images/v2-c53a2eb507dcf761f03e7ef1a5f9ce15_hd.jpg)

测试HTTP接口是应该是这样的：

- 很多单元测试，分别测试各个模块（依赖需要stub）
- 较少的集成测试，测试各个模块之间的交互（依赖不能stub）
- 少量端到端测试，去调用真正地接口（依赖不能stub）

- 最喜欢哪个HTTP框架？为什么？

    这个问题标准答案。需要描述框架的优缺点，这样可以反映开发者对框架的熟悉程度。

## Cookies如何防范XSS攻击？

XSS(Cross-Site Scripting，跨站脚本攻击)是指攻击者在返回的HTTP中插入JavaScript脚本。为了减轻这些攻击，需要在HTTP头部部署`set-cookie`：
- HttpOnly - 这个属性可以防止`cross-site scripting`,因为它禁止javascript脚本访问cookie。

- secure - 这个属性告诉浏览器尽在请求为HTTPS是发送cookie.
    结果应该是这样的：`Set-Cookie:sid=;HttpOnly.`使用Express的话，`cookie-session`默认配置好了。

## 如何保证依赖的安全性？

编写Node.js应用时，很可能依赖成百上千的模块。例如，使用Express的话，会直接依赖[27个模块](https://github.com/expressjs/express/blob/master/package.json#L29)。
因此，手动检查所有的依赖是不现实的。唯一的办法是对依赖进行自动化的安全检查，有这这些工具供选择：

- npm outdated
- Trace by RisingStack
- NSP
- GreenKeeper
- Snyk

## 附加题

### 这段代码有什么问题？

``` node
new Promise(resolve,reject) =>
{
    throw new Error('error')
}
.then(console.log('log'))
```

then柱子后没有catch。这样的话，错误悔会被忽略。
可以这样解决问题：

``` node
new Promise(resolve, reject) =>
{
    throw new Error('error')
}
.then(console.log('log'))
.catch(console.error('error'))
```

调试一个大型项目时，可以使用监控`unhandledRejection`时间来捕获所有未处理的Promise错误：

``` node
process.on('unhandledRejection', (err) =>
{
    console.log(err)
})
```

### 这段代码有什么问题？

``` node
function checkApiKey(apiKeyFromDb, apiKeyReceived)
{
    if(apiKeyFromDb === apiKeyReceived)
    {
        return true;
    }
    return false;
}
```

比较密码时，不能泄露任何信息，因此比较必须在固定时间完成。否则，可以使用[timing attarcks](https://en.wikipedia.org/wiki/Timing_attack, "Timing attack - Wikipedia")来攻击你的应用。**为什么会这样呢？** Node.js使用V8引擎，他会从性能角度优化代码。他会逐个比较字符串的字母，一旦发现不匹配时就停止比较。当攻击者的密码更准确时，比较的时间越长。因此，攻击者可以通过比较的时间长短来判断密码的正确性。使用 **[cryptiles](https://npm.taobao.org/package/cryptiles)** 可以解决这个问题：

```node
function checkApiKey(apiKeyFromDb, apiKeyReceived)
{
    return cryptiles.fixedTimeComparison(apiKeyFromDb, apiKeyReceived)
}
```

### 这段代码的输出是什么？

``` node
Promise.resolve(1)  
.then((x) => x + 1)
.then((x) => { throw new Error('My Error') })
.catch(() => 1)
.then((x) => x + 1)
.then((x) => console.log(x))
.catch(console.error)
```

答案是2，逐行解释如下:

- 创建新的Promise，resolve值为1。

- x为1，加1之后返回2。

- x为2，但是没有用到。抛出一个错误。

- 捕获错误，但是没有处理。返回1。

- x为1，加1之后返回2。

- x为2，打印2。

- 不会执行，因为没有错误抛出。