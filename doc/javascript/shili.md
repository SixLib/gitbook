# 示例

* alert值

``` javascript
window.val = 1;
var json = {
  val: 10,
  sayVal: function() {
    this.val *= 2;
  }
}
json.sayVal();

var b = json.sayVal;
b();


json.sayVal.call(window);

alert(window.val, json.val);
```

* console值

``` javascript
function C1(name){
  if(name) this.name=name;
}
function C2(name){
  console.log(name)
  this.name=name;
}
function C3(name){
  this.name=name||'json'
}

C1.prototype.name='Tom';
C2.prototype.name='Tom';
C3.prototype.name='Tom';
console.log(new C1().name,new C2().name,new C3().name)
```