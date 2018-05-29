
## 作用域
* 函数级作用域
* 变量的查找是就近原则，去寻找var定义的变量，当就近没有找到的时候就去查找外层。
* 当参数跟局部变量重名时，优先级是等同的
* es6块级作用域let 和 const


#### 一、函数级作用域
```js
  var a = 10;
  function aaa () {
    alert(a);
  }
  function bbb () {
    var a = 20;
    aaa();
  }
  bbb();  // 10*/


 function aaa() {
    var a = b = 10;
  }
  aaa();
  alert(b); // 10, 因为a = b = 10 b就等于window.a = 10
```
<br >
#### 二、变量的查找是就近原则，去寻找var定义的变量，当就近没有找到的时候就去查找外层。
```js
  var a = 10;
  function aaa () {
    alert(a); // undefined 查找a的时候会现在函数内查找，由于预解析的作用，此时的a是undefined,因此永远不会去查找外面的10了
    var a = 20;
  }
  aaa();



// 这个吧，虽然是就近原则，但是是就近找var声明的变量，这个是因为没有var声明的变量是全局的，这里只是修改了a的值。所以上面就是因为在函数内没找到var的a，于是到外面去找了，一找就找到了，于是a就alert出10了；不过没错的是a=20后，a确实为20了，只不过alert的时候还没有执行到那~~
 var a = 10
  function aaa () {
    alert(a); // 10
    a = 20
  }
  aaa()
```
<br >
#### 三、当参数跟局部变量重名时，优先级是等同的
```js  
var a = 10
function aaa (a) {
  alert(a); // 10
  var a = 20;
}
aaa(a)
```

###### 其他例子
```js 
var out = 25,
inner = {
  out: 20,
  func: function () {
    var out = 30;
    return this.out;
  }
};

console.log((inner.func, inner.func)());  // 25
console.log(inner.func()); // 20
console.log((inner.func)());  // 20
console.log((inner.func = inner.func)()); // 25*/
```
<br />
#### 四、 es6块级作用域let 和 const
######  1、块级作用域存在域 函数内部和 "{}"之间的区域
```js
{
  let a = 10;
}
console.log(a) // error a is not defined
```
<br >
######  2、同一作用域禁止重复声明
```js
  var count = 30;
  let count = 20; // 抛出语法错误

 let count = 30;
 {
   let count = 20;
   console.log(count); // 20
 }
```
<br >
###### 3、const 是常量用，其值一旦被定义就不可以更改
```js
const a = 10;
a = 20; // 语法错误
```
<br >
###### 4、onst 声明的常量必须进行初始化
```js
 const a; // 语法错误
```
<br >
###### 5、const 其属性可以被修改
```js
const a = {
  b: 12
};

a.b = 13;
console.log(a.b) // 13
```

```js
  var funs = [];
  for (var i = 0; i < 10; i++) {
    funs.push(function() {
      console.log(i)
    });
  }
  funs.forEach((func) => {
    func(); // 输出10次 10
    // 因为循环里每次迭代同时共享着变量i
  })
  
  
  var funs = [];
  for (var i = 0; i < 10; i++) {
    funs.push((function(value) {
      return function () {
        console.log(value);
      }
    })(i));
  }

  funs.forEach((func) => {
    func(); // 输出 0,1,2 .... 9
  })

// 使用let 就很容易实现上面的DEMO

  let funs = [];
  // i 在{}中，所以每次迭代循环都会创建一个新的变量
  for (let i = 0; i < 10; i++) {
    funs.push(function() {
      console.log(i)
    });
  }
  funs.forEach((func) => {
    func(); // 输出 0,1,2 .... 9
  })

```
<br >
###### 6、 const 全局块作用域的绑定
```js
var RegExp = "Hello";
console.log(window.RegExp) // Hello 覆盖window的值


let RegExp = "Hello";
console.log(RegExp); // Hello
console.log('RegExp' in window) // false

```


