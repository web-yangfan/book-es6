
## 扩展对象的功能性
* 对象字面量语法扩展
    * 字面量对象简写
    * 可计算属性名
    * 重复的对象字面量属性
* Object.is()
* Object.assign()
* Object.getPrototypeOf() 和 Object.setPrototypeOf()
* super

#### 对象字面量语法扩展
##### 1. 字面量对象简写
``` js
let preson = {
	name: 'Nicholas',
	sayName() {
		console.log(this.name);
	}
}
```

<br />
##### 2. 可计算属性名
``` js
// 属性名称支持通过任何字符串作为名称访问属性值
let preson = {},
	lastName = 'last name';
preson['first name'] = 'Nicholas';
preson['lastName'] = 'Zakas';


console.log(preson['first name']); // Nicholas
console.log(preson['lastName']);   // Zakas
```
``` js
let lastName = 'last Name';
let proson = {
	'first Name': 'Nicholas',
	[lastName]: 'Zakas'
};
// 中括号将被求值并被最终转化为一个字符串
console.log(proson['first Name']); // Nicholas
console.log(proson[lastName]); // Zakas
```

``` js

let suffix = 'name';

let person = {
    ['first ' + suffix]: 'Nicholas',
    ['last ' + suffix]: 'Zakas'
};

console.log(person['first name']);
console.log(person['last name']);

```
##### 3. 重复的对象字面量属性
###### 重复的属性名称，最后的覆盖前面的
``` js
et person = {
	name: 'Nicholas',
	name: 'Greg',
	name: 'peter'
};
console.log(person.name); // peter

```

<br />

---


#### Object.is()

``` js
/* 
对应Object.is() 方法来说，其运行结果在大部分情况中与 ===运算符相同，
唯一的区别在于+0 和 -0被识别为不相等并且NaN与NaN等价，但是你大可不必抛弃等号运算符,
是否选择用Object.is()方法而不是==或===取决于那些特殊情况如何影响代码。
*/

console.log(+0 == -0); 				// true
console.log(+0 === -0);				// true
console.log(Object.is(+0, -0));		// false

console.log(NaN == NaN);			// false			
console.log(NaN === NaN);			// false
console.log(Object.is(NaN, NaN));	// true

console.log(5 == 5);				// true
console.log(5 == '5');				// true
console.log(5 === 5);				// true
console.log(5 === '5');				// false
console.log(Object.is(5, 5));		// true
console.log(Object.is(5, '5'))		// false
```
<br />

---

#### Object.assign()
###### Object.assign() 方法可以接受任意数量的源对象，并按指定的顺序将属性复制到接收对象中，所以如果多个源对象具有同名属性，则排位靠后的对象会覆盖排位靠前的，如下代码
``` js
let receiver = {};
Object.assign(receiver, 
	{
		type: 'js',
		name: 'file.js'
	},
	{
		type: 'css'
	}
);
console.log(receiver.type); // 'css'
console.log(receiver.name); // 'file.js'
```

<br />

---

#### Object.getPrototypeOf() 和 Object.setPrototypeOf()
###### Object.getPrototypeOf() 返回任意知道对象的原型
###### Object.setPrototypeOf() 改变任意指定对象的原型
``` js
let person = {
		getGreeting() {
			return 'Hello';
		}
	};

	let dog = {
		getGreeting() {
			return 'woof';
		}
	}

	// 以person 对象为原型
	let friend = Object.create(person);
	console.log(friend.getGreeting());
	console.log(Object.getPrototypeOf(friend) === person);

	// 将原型设置为 dog
	Object.setPrototypeOf(friend, dog);
	console.log(friend.getGreeting());
	console.log(Object.getPrototypeOf(friend) === dog);

```

<br />

---

#### super

``` js

let person = {
		getGreeting() {
			return 'Hello'
		}
	};

	let friend = {
		getGreeting() {
			return super.getGreeting() + ' hi';
		}
	}

	// 将原型设置为person
	Object.setPrototypeOf(friend, person);
	console.log(friend.getGreeting()); // Hello hi

```

###### 如果想重写对象的实例方法，有需要调用与它同名的原型方法，可以这样实现(ES5的写法)：
``` js
let person = {
		getGreeting() {
			return 'Hello'
		}
	};

	let dog = {
		getGreeting() {
			return 'Woof'
		}
	}

	let friend = {
		getGreeting() {
			return Object.getPrototypeOf(this).getGreeting.call(this) + ' hi';
		}
	}

	// 将原型设置为person
	Object.setPrototypeOf(friend, person);
	console.log(friend.getGreeting());	// Hello hi
	console.log(Object.getPrototypeOf(friend) === person);  // true

	// 将原型设置为dog
	Object.setPrototypeOf(friend, dog);
	console.log(friend.getGreeting()); // Woof hi
	console.log(Object.getPrototypeOf(friend) === dog); // true
```

###### 上面的在多重继承的情况下会出错
``` js
let person = {
		getGreeting() {
			return 'Hello'
		}
	};


	let friend = {
		getGreeting() {
			return Object.getPrototypeOf(this).getGreeting.call(this) + ' hi';
		}
	}

	// 将原型设置为person
	Object.setPrototypeOf(friend, person);
	
	// 原型是friend
	let relative = Object.create(friend);

	console.log(person.getGreeting()); // Hello
	console.log(friend.getGreeting()); // Hello hi

	// this是relative，relative的原型是friend对象，当执行relative.getGreeting方法时，会调用friend的getGreeting()方法，而此时的this值为relative，Object.getPrototypeOf(this)又会返回friend对象，所以就会进入递归调用直到触发栈溢出报错
	console.log(relative.getGreeting()); // error !
```
###### 使用super可以解决上面的问题
``` js
let person = {
		getGreeting() {
			return 'Hello'
		}
	};


	let friend = {
		getGreeting() {
			return super.getGreeting() + ' hi';
		}
	}

	// 将原型设置为person
	Object.setPrototypeOf(friend, person);
	
	// 原型是friend
	let relative = Object.create(friend);

	console.log(person.getGreeting()); // Hello
	console.log(friend.getGreeting()); // Hello hi
	console.log(relative.getGreeting()); // Hello hi
	
```


