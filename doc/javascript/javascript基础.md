# Javascript 基础

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

* [Javascript 基础](#javascript-基础)
	* [JavaScript 对象](#javascript-对象)
		* [Array 对象](#array-对象)
			* [数组属性](#数组属性)
				* [length](#length)
				* [prototype](#prototype)
			* [对象属性](#对象属性)
				* [concat()方法](#concat方法)
				* [every()方法](#every方法)
				* [some()方法](#some方法)
				* [filter()方法](#filter方法)
				* [forEach()方法](#foreach方法)
				* [indexOf()方法](#indexof方法)
				* [isArray()方法](#isarray方法)
				* [join()方法](#join方法)
				* [toString()方法](#tostring方法)
				* [lastIndexOf()方法](#lastindexof方法)
				* [map()方法](#map方法)
				* [pop()方法](#pop方法)
				* [push()方法](#push方法)
				* [unshift()方法](#unshift方法)
				* [reverse() 方法](#reverse-方法)
				* [shift()方法](#shift方法)
				* [slice()方法](#slice方法)
				* [sort()方法](#sort方法)
				* [splice()方法](#splice方法)
		* [String 对象](#string-对象)
			* [对象方法](#对象方法)
				* [charAt(index)方法](#charatindex方法)
				* [charCodeAt(index)方法](#charcodeatindex方法)
				* [concat(item1,item2...itemX)方法](#concatitem1item2itemx方法)
				* [fromCharAt(n1,n2...nX)方法](#fromcharatn1n2nx方法)
				* [indexOf(searchvalue,index)方法](#indexofsearchvalueindex方法)
				* [lastIndexOf(searchvalue, index)方法](#lastindexofsearchvalue-index方法)
				* [match(regexp)方法](#matchregexp方法)
				* [replace(searchvalue,newvalue)方法](#replacesearchvaluenewvalue方法)
				* [slice(start,end)方法](#slicestartend方法)
				* [split(separator,limit)方法](#splitseparatorlimit方法)

<!-- /code_chunk_output -->

## JavaScript 对象

### Array 对象

``` javascript
var arr = ['Saab', 'Volvo', 'BMW']
```

#### 数组属性

##### length

> 设置、返回数组的长度（数组中元素的数目）。

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.length);
//输出：4

fruits.length=5;
console.log(fruits.toString());
//输出：Banana,Orange,Apple,Mango,
```

##### prototype

>prototype 属性使您有能力向对象添加属性和方法。
> 当构建一个属性，所有的数组将被设置属性，它是默认值。
> 在构建一个方法时，所有的数组都可以使用该方法。
> 注意： Array.prototype 单独不能引用数组, Array() 对象可以。
> 注意： 在JavaScript对象中，Prototype是一个全局属性。

``` javascript
Array.prototype.myUcase=function()
{
    for (i=0;i<this.length;i++)
    {
        this[i]=this[i].toUpperCase();
    }
}
var fruits=["Banana","Orange","Apple","Mango"];
fruits.myUcase();
console.log(fruits.sort().toString());
//输出：APPLE,BANANA,MANGO,ORANGE
```

#### 对象属性

##### concat()方法

> 连接多个数组，不破坏源数组的情况下生成新的数组

``` javascript
var hege = ["Cecilie", "Lone"];
var stale = ["Emil", "Tobias", "Linus"];
var kai = ["Robin"];
var children = hege.concat(stale,kai);
console.log(children)
//children 输出 Cecilie,Lone,Emil,Tobias,Linus,Robin
```

##### every()方法

> 验证数组中元素是否满足条件,返回值 boolean类型；**不能对空数组进行检测**

``` javascript
var ages = [32, 33, 16, 40];

function checkAdult(age) {
    return age >= 18;
}
console.log(ages.every(checkAdult))
//输出false
```

##### some()方法

> 用于检查数组中元素是否有满足指定条件（函数）；只要有一个元素满足则返回true,如果没有元素满足条件则返回false.

``` javascript
var ages = [3, 10, 18, 20];

function checkAdult(age) {
    return age >= 18;
}
console.log(ages.some(checkAdult))
//输出：true

function checkAdult1(age) {
    return age >= 21;
}
console.log(ages.some(checkAdult1))
//输出：false

```

##### filter()方法

> 创建一个新数组，新数组是指定数组中满足条件的远足组成的数组；

``` javascript
var ages = [32, 33, 16, 40];

function checkAdult(age) {
    return age >= 18;
}
console.log(ages.filter(checkAdult))
//输出 ： 32，33，40
```

##### forEach()方法

> 用于调用数组中的每一个元素，并将元素传递给回调函数。**对空数组不调用回调函数的。**

``` javascript
var numbers = [4, 9, 16, 25];
function myFunction(item, index) {
     console.log(item) 
}
numbers.forEach(myFunction)
/**
 * 输出：
 * 4
 * 9
 * 16
 * 25
 */
```

##### indexOf()方法

> 返回数组中某个指定元素第一次出现的位置；**没有找到指定元素则返回-1。**

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.indexOf("Apple"))
//输出 2

console.log(fruits.indexOf("pint"))
//输出 -1
```

##### isArray()方法

> 判断一个对象是否是数组；返回boolean类型值。

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(Array.isArray(fruits));
//输出： true
console.log(Array.isArray({}));
//输出： false
```

##### join()方法

> 将数组中所有元素转换成一个字符串。

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.join())
//输出： Banana,Orange,Apple,Mango

console.log(fruits.join(" and "))
//输出： Banana and Orange and Apple and Mango

```

##### toString()方法

> 将数组转换为以`,`分割的字符串,并返回结果。

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.sort().toString());
//输出：Apple,Banana,Mango,Orange
```

##### lastIndexOf()方法

> 在一个数组中从后向前搜索，返回一个指定元素在数组中最后出现的位置。**没有找到指定元素则返回-1。**

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.lastIndexOf("Apple"))
//输出 2

console.log(fruits.lastIndexOf("pint"))
//输出 -1
```

##### map()方法

> 按照原始数组元素顺序依次处理元素，返回一个新数组，新数组中的元素为y原始数组调用函数处理后的值。

``` javascript
var numbers = [4, 9, 16, 25];
var newNumb = numbers.map(Math.sqrt)
/**
 * item 元素对象
 * index 索引
 * arr 源数组
 */
newNumb.map(function(item, index, arr){
    console.log(item)
    console.log(index)
    console.log(arr)
})
```

##### pop()方法

> 删除数组中最后一个元素并返回删除的元素。

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.pop());
//输出：Mango

console.log(fruits.join());
//输出：Banana,Orange,Apple
```

##### push()方法

> 可向数组的末尾添加一个或多个元素，并返回一个新的长度。此方法改变数组的长度。

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.push("Kiwi","Betel nut")
console.log(fruits.join())
//输出：Banana,Orange,Apple,Mango,Kiwi,Betel nut
```

##### unshift()方法

> 方法可向数组的开头添加一个多个元素，并返回添加之后的数组长度。

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
var fruitsLength=fruits.unshift("Lemon","Pineapple");
console.log(fruitsLength);
//输出：6

console.log(fruits.toString());
//输出：Lemon,Pineapple,Banana,Orange,Apple,Mango

```

##### reverse() 方法

> 用于颠倒数组中元素的顺序。

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.reverse();
console.log(fruits.join())
//输出：Mango,Apple,Orange,Banana
```

##### shift()方法

> 用于把数组中的第一个元素从其中删除，并返回第一个元素。

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
console.log(fruits.shift())
//输出：Banana

console.log(fruits.join())
//输出：Orange,Apple,Mango
```

##### slice()方法

> 从已有的数组中返回选定的元素；可根据索引范围返回新的数组，不破坏原数组。

``` javascript
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
console.log(fruits.slice(1,3).join());
//输出：Orange,Apple
```

##### sort()方法

> 用于对数组中的元素进行排序；排序顺序可以是字母或数字，并按升序或降序。
> 注意：当数字是按字母顺序排列时"40"将排在"5"前面。
> 使用数字排序，你必须通过一个函数作为参数来调用。
> 函数指定数字是按照升序还是降序排列。
> 这些说起来可能很难理解，你可以通过本页底部实例进一步了解它。
> 注意： 这种方法会改变原始数组！

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
//默认排序顺序为按字母升序。
console.log(fruits.sort().join());
//升序输出：Apple,Banana,Mango,Orange

console.log(fruits.sort().reverse().join());
//降序输出：Orange,Mango,Banana,Apple

var points = [40,100,1,5,25,10];
function sortfunc (a,b){
    return a-b;
}
console.log(points.sort(sortfunc).join())
//升序输出：1,5,10,25,40,100

function sortfunc1 (a,b){
    return b-a;
}
console.log(points.sort(sortfunc1).join())
//降序输出：100,40,25,10,5,1
```

##### splice()方法

> splice(index,howmany,item1...itemX)
> index 规定从何处添加、删除元素（必须）；必须为数字。
> howmany 规定删除多少元素（必须）；必须为数字。
> item1...itemX 要添加到数组中的新元素（可选）。
> **该方法会破坏原数组。**

``` javascript
var fruits = ["Banana", "Orange", "Apple", "Mango"];

//在下标为2的位置向后删除0个元素，出入两个元素
fruits.splice(2,0,"Lemon", "Kiwi");
console.log(fruits.join());
//输出：Banana,Orange,Lemon,Kiwi,Apple,Mango

//在下标为2的位置向后删除2个元素
fruits.splice(2,2);
console.log(fruits.join());
//输出：Banana,Orange,Apple,Mango
```

### String 对象

#### 对象方法

##### charAt(index)方法

> 返回指定位置的字符。

``` javascript
var str = "HELLO WORLD";
console.log(str.charAt(2))
//输出：L
```

##### charCodeAt(index)方法

> 返回指定位置的字符的 Unicode编码。

``` javascript
var str = "HELLO WORLD";
console.log(str.charCodeAt(2))
//输出：76
```

##### concat(item1,item2...itemX)方法

> 连接两个或多个字符串；不破坏原字符串。（性能问题不建议使用，建议使用操作符‘`+、+=`’ 代替）

``` javascript
var str1 = "Hello ";
var str2 = "world!";
var str3 = "hey hey";
var n =str1.concat(str2,str3)
console.log(n);
//输出："Hello world!hey hey"
```

##### fromCharAt(n1,n2...nX)方法

> 将 一个或多个 Unicode 编码转为字符。

``` javascript
var n = String.fromCharCode(72,69,76,76,79);
console.log(n);
//输出：HELLO
```

##### indexOf(searchvalue,index)方法

> 从指定位置开始查询指定字符所在位置；index为起始查询位置，非必填，从头开始查找。

``` javascript
var str="Hello world, welcome to the universe.";
var n=str.indexOf("e");
console.log(n);
//输出：1

n=str.indexOf("e",3);
console.log(n)；
//输出：14
```

##### lastIndexOf(searchvalue, index)方法

> 返回一个指定字符串值最后出现的位置;index为起始查询位置，非必填，从末尾开始查找。

``` javascript
var str="I am from runoob，welcome to runoob site.";
var n=str.lastIndexOf("runoob");
console.log(n);
//输出：28

var m=str.lastIndexOf("runoob",20);
console.log(m);
//输出：10
```

##### match(regexp)方法

> 根据正则表达式匹配出字符串或数组；
> regexp 表达式中包含g时，返回一个元素为匹配的内容的数组；否则，只执行一次，查找到返回字符串，否则返回null.

``` javascript
var str="The rain in SPAIN stays mainly in the plain";
var array=str.match(/ain/gi);
console.log(array.toString());
//输出："ain,AIN,ain,ain"
```

##### replace(searchvalue,newvalue)方法

> 在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的字符串。

``` javascript
var str="Visit Microsoft! Visit microsoft!";
var n=str.replace("Microsoft","Runoob");
console.log(n);
//输出：Visit Runoob! Visit microsoft!

var str1="Mr Blue has a blue house and a blue car";
var m=str1.replace(/blue/g,"red");
console.log(m);
//输出：Mr Blue has a red house and a red car

m=str1.replace(/blue/gi, "red");
console.log(m);
//输出：Mr red has a red house and a red car
```

##### slice(start,end)方法

> 可提取字符串的某个部分，并以新的字符串返回被提取的部分。

``` javascript
var str="Hello world!";
var n=str.slice(1,5);
console.log(n)
//输出：ello

n=str.slice(6);
console.log(n);
//输出：world!

console.log(str.slice(-1));
//输出：！
```

##### split(separator,limit)方法

> 将字符串分割成数组；separator为分割规则（非必须），limit定义了返回的数组长度（非必须）。

``` javascript
var str="How are you doing today?";
console.log(str.split());
//输出：["How are you doing today?"]

console.log(str.split(""));
//输出：["H", "o", "w", " ", "a", "r", "e", " ", "y", "o", "u", " ", "d", "o", "i", "n", "g", " ", "t", "o", "d", "a", "y", "?"]

console.log(str.split(" "));
//输出:["How", "are", "you", "doing", "today?"]

console.log(str.split(" ",3));
//输出:["How", "are", "you"]

```

