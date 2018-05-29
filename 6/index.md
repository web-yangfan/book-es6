## 改进数组的功能(ES6 和 ES5的数组方法)
* Array.of()
* Array.from()
* find() 和 findIndex() 方法
* includes()
* forEach (js v1.6)
* map (js v1.6)
* filter (js v1.6)
* some (js v1.6)
* every (js v1.6)
* indexOf (js v1.6)
* lastIndexOf (js v1.6)
* reduce (js v1.8)
* reduceRight (js v1.8)
* 数组去重
* 复制数组
* 连接数组

#### Array.of()方法用于将一组值，转换为数组
###### 以下是Array 构造函数创建数组时候的怪异行为
``` js
let items = new Array(2);
console.log(items.length); // 2
console.log(items[0]);  // undefined
console.log(items[1]);  // undefined

let items = new Array("2");
console.log(items.length); // 1
console.log(items[0]);  // "2"

let items = new Array(1, 2);
console.log(items.length); // 2
console.log(items[0]);  // 1
console.log(items[1]);  // 2


let items = new Array(3, "2");
console.log(items.length);  // 2
console.log(items[0]);		// 3
console.log(items[1]);		// "2"
```
###### ECMAScript 6 Array.of() 解决上面的怪异行为
``` js

let items = Array.of(1, 2);
console.log(items.length); // 2
console.log(items[0]); // 1
console.log(items[1]); // 2

let items = Array.of(2);
console.log(items.length); // 1
console.log(items[0]); // 2

let items = Array.of("2");
console.log(items.length); // 1
console.log(items[0]); // "2"

```

<br />


-------

#### Array.from()法用于将两类对象转为真正的数组：类数组的对象（ array-like object ）和可遍历（ Iterable ）的对象（包括 ES6 新增的数据结构 Set 和Map ）。

``` js
let arrayLike = {  
　　'0': 'a',  
　　'1': 'b',  
　　'2': 'c',  
　　length: 3  
};  
// ES5 的写法  
var arr1 = [].slice.call(arrayLike); // [‘a‘, ‘b‘, ‘c‘]  
// ES6 的写法  
let arr2 = Array.from(arrayLike); // [‘a‘, ‘b‘, ‘c‘]  

console.log(arr1);  // [‘a‘, ‘b‘, ‘c‘]  
console.log(arr2);  // [‘a‘, ‘b‘, ‘c‘]  


// NodeList 对象  
let item = Array.from(document.querySelectorAll('p'));  
item.forEach(function (p) {  
　　console.log(p);  
});  


// arguments 对象  
function foo() {  
	var args = Array.from(arguments);  
	// ...  
}  

//字符串转换为字符数组str.split('')  
Array.from('hello')  // ['h', 'e', 'l', 'l', 'o']  
let namesSet = new Set(['a', 'b'])  
Array.from(namesSet) // ['a', 'b']  
  
Array.from({ length: 3 });  // [ undefined, undefined, undefined ] 


// Array.from还可以接受第二个参数，作用类似于数组的map方法，用来对每个元素进行处理，将处理后的值放入返回的数组。
function translate() {
	return Array.from(arguments, (value) => value + 1);
}

let numbers = translate(1, 2, 3);  // [2, 3, 4]
console.log(numbers);
```
<br />


-------


#### find() 和 findIndex() 方法
* 一个参数是回调参数
* 二个参数可选参数 
* 满足条件立即停止，find返回查到的值，findIndex返回索引


``` js
let numbers = [25, 30, 35, 40, 45];
console.log(numbers.find( n => n > 33)); // 35
console.log(numbers.findIndex( n => n > 33)); // 2

```

<br />

-------


#### includes() 检查数组包含某个值 方法返回一个布尔值

``` js
 [1, 2, 3].includes(2);     // true
 [1, 2, 3].includes(4);     // false
 [1, 2, NaN].includes(NaN); // true
 
```

<br />


-------

#### forEach (js v1.6)

``` js
/*
 * 遍历，循环
 * array.forEach(callback,[ thisObject])
 * */
var arr = ['艾斯','路飞','娜美','山治','弗兰奇','香克斯'];
arr.forEach(function(item,index){
  console.log(index+'---'+item)
})


var database = {
  arr : ['艾斯','路飞','娜美','山治','弗兰奇','香克斯'],
  console:function(name){
    console.log(this.addStr(name))
  },
  addStr:function(name){
    return '姓名：'+ name;
  }
};

database.arr.forEach(database.console,database)

/* 输出:
  姓名：艾斯
  姓名：路飞
  姓名：娜美
  姓名：山治
  姓名：弗兰奇
  姓名：香克斯
  */
```

<br />


-------
#### map (js v1.6)

``` js
/*
 * map 原数组被“映射”成对应新数组
 * array.map(callback,[ thisObject]);
 * */
var arr = [1,2,3,4,5];
var newArr = arr.map(function(item){
  return item * item
})
console.log(newArr)  //[1,4,9,16,25]
```

<br />


-------
#### filter (js v1.6)

``` js
/*
* filter 筛选、过滤
* array.filter(callback,[ thisObject]);
* */
var arr = [1,2,3,1,4,5,1];
var newArr = arr.filter(function(item){
  return item !=1;
})
console.log(newArr)  //[2,3,4,5]

```

<br />


-------
#### some (js v1.6)

``` js
/*
* some 指是否“某些项”合乎条件,some只有有true即返回不再执行了。
* array.some(callback,[ thisObject]);
* */
var arr = [1,2,3,1,4];
var current = 1;

function higherThanCurrent(score) {
  return score > current;
}

if (arr.some(higherThanCurrent)) {
  console.log("朕准了！");  //就输出一次
}

```

<br />


-------
#### every (js v1.6)

``` js

/*
* every 指是否“某些项”合乎条件,every只有都为true才会返回true
* array.every(callback,[ thisObject]);
* */
var arr = [2,2,3,2,4];
var current = 1;

function higherThanCurrent(score) {
  return score > current;
}

if (arr.every(higherThanCurrent)) {
  console.log("朕准了！");  //就输出一次
} else {
  console.log("来人，拖出去斩了！");
}

```

<br />


-------
#### indexOf (js v1.6)

``` js

/*
* indexOf 判断是否存在，存在返回索引值,不存在返回 -1
* array.indexOf(searchElement[, fromIndex])
 * */
var arr = [1,2,3,4,5];
var index = arr.indexOf(10)
console.log(index)

```

<br />


-------
#### lastIndexOf (js v1.6)

``` js
/*
* lastIndexOf
* lastIndexOf方法与indexOf方法类似只是lastIndexOf是从字符串的末尾开始查找，而不是从开头。还有一个不同就是fromIndex的默认值是array.length - 1而不是0.
* array.lastIndexOf(searchElement[, fromIndex])
* */
var data = [2, 5, 7, 3, 5];

console.log(data.lastIndexOf(5)); // 4
console.log(data.lastIndexOf(5, 3)); // 1 (从后往前，索引值小于3的开始搜索)

console.log(data.lastIndexOf(4)); // -1 (未找到)

```

<br />


-------
#### reduce (js v1.8)

``` js
 /*
 * reduce
 *callback函数接受4个参数：之前值、当前值、索引值以及数组本身。initialValue参数可选，表示初始值。若指定，则当作最初使用的previous值；如果缺省，则使用数组的第一个元素作为previous初始值，同时current往后排一位，相比有initialValue值少一次迭代。
 * array.reduce(callback[, initialValue])
 * */

 var sum = [1, 2, 3, 4].reduce(function (previous, current, index, array) {
   return previous + current;
 });

 console.log(sum); // 10
/* 说明：

 1、因为initialValue不存在，因此一开始的previous值等于数组的第一个元素。
 2、从而current值在第一次调用的时候就是2.
 3、最后两个参数为索引值index以及数组本身array.

 以下为循环执行过程：
 // 初始设置
 previous = initialValue = 1, current = 2

 // 第一次迭代
 previous = (1 + 2) =  3, current = 3

 // 第二次迭代
 previous = (3 + 3) =  6, current = 4

 // 第三次迭代
 previous = (6 + 4) =  10, current = undefined (退出)
 */

// 有了reduce，我们可以轻松实现二维数组的扁平化：



 var matrix = [
   [1, 2],
   [3, 4],
   [5, 6]
 ];

 // 二维数组扁平化
 var flatten = matrix.reduce(function (previous, current) {
   return previous.concat(current);
 });

 console.log(flatten); // [1, 2, 3, 4, 5, 6]

```

<br />


-------
#### reduceRight (js v1.8)

``` js
 /*
 * reduceRight
 * educeRight跟reduce相比，用法类似,实现上差异在于reduceRight是从数组的末尾开始实现
 * array.reduceRight(callback[, initialValue])
 * */

 var data = [1, 2, 3, 4];
 var specialDiff = data.reduceRight(function (previous, current, index) {
   if (index == 0) {
     return previous + current;
   }
   return previous - current;
 });

 console.log(specialDiff); // 0
/* 结果0是如何得到的呢？
 我们一步一步查看循环执行：

 // 初始设置
 index = 3, previous = initialValue = 4, current = 3

 // 第一次迭代
 index = 2, previous = (4- 3) = 1, current = 2

 // 第二次迭代
 index = 1, previous = (1 - 2) = -1, current = 1

 // 第三次迭代
 index = 0, previous = (-1 + 1) = 0, current = undefined (退出)
 */

// 有了reduce，我们可以轻松实现二维数组的扁平化：

```

<br />


-------

#### 数组去重
``` js
/*
 * 去除数组重复成员
 * */
function dedupe(array) {
  // Array.from方法可以将Set结构转为数组
  return Array.from(new Set(array));
}
dedupe([1, 1, 2, 3]) // [1, 2, 3]

let arr = [3, 5, 2, 2, 5, 5];
let unique = [...new Set(arr)];
// unique  [2, 5, 2]
```

<br />


-------

#### 复制数组
``` js
const names = ['Luke','Eva','Phil'];
const copiedList = [...names]  
console.log(copiedList); // ['Luke','Eva','Phil']


// 这里复制的是引用。也就是说如果一个数组中的元素发生改变，那么另一个数组中的元素也相应地发生改变。
var initialArray = [{name: "Luke"}];
var copiedArray = [...initialArray];

initialArray[0]['name'] = 'Mark';
console.log(initialArray); //Array [{'name': 'Mark'}]
console.log(copiedArray); //Array [{'name': 'Mark'}]

```
<br />


-------

#### 连接数组
``` js
const concatinated = [...names, ...names];
console.log(concatinated); 
// ['Luke','Eva','Phil', 'Luke','Eva','Phil']


const first = ['Emily', ...names];  
console.log(first); // ['Emily','Luke','Eva','Phil']

const last = [...names, 'Emily'];  
console.log(last); // ['Luke','Eva','Phil', 'Emily']
```


