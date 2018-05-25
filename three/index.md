## 函数

1. 默认参数
	* 使用默认参数
	* 默认参数表达式
	* 不定参数
	* 解构参数
	* 默认参数值对arguments的影响
2. 箭头函数
<br >
----

### 默认参数
####1. 使用默认参数

``` js
function makeRequest (url, timeout = 2000, callback = function () {}) {

};

// 使用timeout和callback 参数为默认值
makeRequest('/foo');

// 使用callback 参数为默认参数
makeRequest('/foo', 500);

// 不使用默认参数
makeRequest('/foo', 500, function (body) {
  console.log(body);
});

// 不使用timeout的默认值
makeRequest('/foo', null, function (body) {

});

// 不使用timeout的默认值
makeRequest('/foo', undefined, function (body) {

});

``` 
<br >
#### 2. 默认参数表达式

``` js
function addFirst(first, second = first + 1) {
	return first + second;
};
console.log(addFirst(1)); // 3

function addSecond(first, second = first) {
	return addSecond + second;
};
console.log(add(1)); // 2

function addThree (first = second, second) {
	console.log(first);
	return first + second;
}
// 因为默认参数的临时死区 抛出异常
/*
 表示调用addThree(undefined, 1)的 javascript 代码：
 let first = second;
 let second = 1;
 所有会报错
*/
console.log(addThree(undefined, 1)); 
```
<br >
#### 3. 不定参数
1. 不定蚕食为一个数组
2. 每个函数只能声明一个不定参数
3. 不定参数一定要在所有参数的末尾
4. 不定参数不能用于对象字面量setter之中

``` js
function pick (first, ...second) {
	console.log(first); // 1
	console.log(second); // [3, 4, 5, 6]
};

pick(2, 3, 4, 5, 6);

let pick = {
	set getValue (...value) {
		console.log(value); // 抛出异常
	}
};
pick.getValue(1, 2, 3, 4, 5);
```

<br >

#### 4. 解构参数
``` js
function setCookie(name, vlaue, { secure, path, domain, expires}) {
	console.log(name);   // type
	console.log(vlaue);  // js
	console.log(secure); //  true
	console.log(path);   //  undefined
	console.log(domain); //  undefined
	console.log(expires); // 60000
}

setCookie('type', 'js', {
	secure: true,
	expires: 60000
});

```


<br >

#### 5. 默认参数值对arguments的影响

``` js
// first和second被赋予新值，arguments[0]和 arguments[1]相应地也更新了
// 在ECMAScript5的严格模式，argument对象不会随之改变
function mixArgs (first, second) {
  console.log(first === arguments[0]);  // true
  console.log(second === arguments[1]); // true
  first = 'c';
  second = 'd';
  console.log(first === arguments[0]); // true
  console.log(second === arguments[1]) // true
}

mixArgs('a', 'b');




// ECMAScript6中 函数使用了默认参数值argument对象不会随着参数值改变而改变
function mixArgs (first, second = 'y') {
  console.log(first === arguments[0]); // true
  console.log(second === arguments[1]); // true
  first = 'c';
  second = 'd';
  console.log(first === arguments[0]);  // false
  console.log(second === arguments[1]); // false
}

mixArgs('a', 'b');
```

<br >

----

### 箭头函数
* 箭头函数没有 this、super、arguments、new.target，箭头函数中的this、super、arguments、new.target这些值由外围最近一层非箭头函数决定的
* 不能通过new关键字调用，箭头函数没有[[Construct]]
* 没有原型
* 不支持重复的命名参数


###### <font color="#9E1316">箭头函数语法多变所有变种都由：函数参数、箭头、函数体组成</font>

``` js
let reflect = value => value;
// 等于
let reflect = function (value) {
	return value;
};


let sum = (num1, num2) => num1 + num2;
// 等于
let sum = function (num1, num2) {
	return num1 + num2;
}


let getName = () => 'Nicholas';
// 等于
let getName = function () {
	return 'Nicholas';
}


let sum = (num1, num2) => {
	return num1 + num1;
}
// 等于
let sum = function (num1, num2) {
	return num1 + num2;
}

let  getTempItem = id => ({id: id, name: 'Temp'})
// 等于
let getTempItem = function (id) {
	return {
		id: id,
		name: 'Temp'
	};
};

// 立即执行函数
let person = ((name) => {
	return {
		getName: function () {
			return name;
		}
	}
})('Nicholas');

console.log(person.getName()); // Nicholas
```

