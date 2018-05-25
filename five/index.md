* 基本用法
* 解构赋值
* 默认值
* 赋值变量起别名
* 嵌套解构
* 不定数组元素
* 数组混合解构
* 解构参数

##### 1. 基本用法
``` js
// 对象解构
let node = {
	type: 'Identifier',
	name: 'foo'
};
let { type, name } = node;
console.log(type); // 'Identifier'
console.log(name); // foo


let colors = [ 'red', 'green', 'grey'];
let [ firstColor, secondColor] = colors;
console.log(firstColor); // red
console.log(secondColor); // green

// 数组解构是根据顺序赋值的
let colors = [ 'red', 'green', 'grey'];
let [ , , third] = colors;
console.log(third); // green

```
##### 2. 解构赋值
``` js
// 解构赋值
let node = {
	type: 'Identifier',
	name: 'foo'
},
type = 'Literal',
name = 'peter';

// 使用解构语法为多个变量赋值
// 代码块语句不允许出现在赋值语句的左侧
// 加上小括号将代码块语句转换成一个表达式
({ type, name } = node);

console.log(type); // 'Identifier'
console.log(name); // foo


let colors = [ 'red', 'green', 'grey'],
	firstColor = 'blue',
	secondColor = 'yellow';

	[ firstColor, secondColor] = colors;
	console.log(firstColor); // red
	console.log(secondColor); // green
	
// 交换变量
let a = 1, b = 2;
[a, b] = [b, a];
console.log(a); // 2
console.log(b); // 1

```
##### 3. 默认值
``` js
let node = {
	type: 'Identifier',
	name: 'foo'
};

let { type, name, value = true, age} = node;

console.log(type);	// Identifier
console.log(name);	// foo
console.log(value);	// true
console.log(age); // undefined


let colors = [ 'red',];
let [ firstColor, second = "green"] = colors;
console.log(firstColor); // red
console.log(second); // green
```
##### 4. 赋值变量起别名

``` js
let node = {
	type: 'Identifier',
	name: 'foo'
};

let { type: localType, name: localName, age: localAge = '24'} = node;

console.log(localType);	// Identifier
console.log(localName);	// foo
console.log(localAge);	// 24
```

##### 5. 嵌套解构
``` js
let node = {
	type: 'Identifier',
	name: 'foo',
	loc: {
		start: {
			line: 1,
			colunm: 2
		},
		end: {
			line: 1,
			colunm: 2
		}
	}
}
	
let {loc: { start }} = node;
let {loc: { end:localEnd }} = node;

console.log(start.line);	// 1
console.log(start.colunm);	// 2

console.log(localEnd.line);	// 1
console.log(localEnd.colunm); // 2



let colors = [ 'red', ['green', 'lightgreen'], 'blue' ];

let [ firstColor, [ secondColor] ] = colors;

console.log(firstColor);   // red
console.log(secondColor);  // green
```


#### 6. 不定数组元素
``` js
let colors = ['red', 'green', 'grey', 'blue'];

let [ firstColor, ...secondColor] = colors;
console.log(firstColor); // red
console.log(secondColor[0]); // green
console.log(secondColor[1]); // grey
console.log(secondColor[2]); // blue 


// 复制数组
let colors = ['red', 'green', 'grey', 'blue'];
let [ ...secondColor] = colors;

console.log(secondColor); // ["red", "green", "grey", "blue"]	
```

##### 7. 数组混合解构

``` js
let node = {
	type: 'Identifier',
	name: 'foo',
	loc: {
		start: {
			line: 1,
			column: 1
		},
		end: {
			line: 1,
			column: 4
		}
	},
	range: [0, 3]
};

let { loc: {start},
	range: [ startIndex ]
} = node;
console.log(start.line);   // 1
console.log(start.column); // 1
console.log(startIndex);   // 0
```

#### 8. 解构参数
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

