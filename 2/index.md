## 字符串

* 模板字符串
* includes()
* startsWith()
* endsWith()
* repeat()
* padStart()，padEnd()
<br />


-------
#### 模板字符串
``` js
let json = {
  name: '艾斯'
}

let age = 23

let gender = () => {
  return '男'
}

let str = `我的名字是：${json.name}，我的性别是:${age}，我的年纪是:${gender()}`;
console.log(str) // 我的名字是：艾斯，我的性别是:23，我的年纪是:男

```

<br />


-------

#### includes()
###### 返回布尔值，表示是否找到了参数字符串。

``` js
var s = 'Hello world';
s.includes('o'); // true

// 第二个参数，表示开始搜索的位置
s.includes('Hello', 6); // false



```
<br />


-------

#### startsWith()
###### 返回布尔值，表示参数字符串是否在源字符串的头部。

``` js
var s = 'Hello world';
s.startsWith('Hello'); // true

// 第二个参数，表示开始搜索的位置
s.startsWith('world', 6); // true

```
<br />


-------

#### endsWith()
###### 返回布尔值，表示参数字符串是否在源字符串的尾部

``` js
var s = 'Hello world';
s.endsWith('!'); // false

// 第二个参数，表示开始搜索的位置
s.endsWith('Hello', 5)； // true

```

<br />


-------

#### repeat()
###### 返回一个新字符串，表示将原字符串重复n次

``` js
'x'.repeat(3);  // xxx

```

<br />


-------

#### padStart()，padEnd()
###### 字符串补全长度的功能

``` js
'x'.padStart(4, 'ab') // 'abax'
'x'.padEnd(5, 'ab') // 'xabab'

```

<br />


-------