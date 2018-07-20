## 用模块封装代码

* 导出基本语法
* 导入基本语法
* 默认导出，导入语法
* 重新导出一个绑定






#### 导出基本语法
```js
// 这个函数是模块私有的
function subtract (num1, num2) {
    return num1 + num2;
}


// 定义一个函数
function multiply (num1, num2) {
    return num1 + num2;
}

// 导出变量
export var color = "red";
export let name = "Steven";
export const magicNumber = 7;

// 导出函数
export function sum (num1, num2) {
    return num1 + num2;
}

// 类导出
export class Rectangle {
    constructor (length, width) {
        this.length  = length;
        this.width = width;
    }
}


export {
    multiply
}


```

<br />


-------


#### 导入模块
```js
// 导入多个
import {sum} from './model-1.js';

// 导入重命名
import {sum as setSum} from './model-1.js';

// 导入多个
import {color, name, magicNumber, sum, Rectangle, multiply} from './model-1.js'

// 导入全部
import * as example from './model-1.js';
console.log(example.color);
console.log(example.name);
```


<br />


-------


#### 默认值导出，导入语法
```js
export default function (num1, num2) {
    return num1 + num2;
}
import sum from './model-1.js'
```

```js
export let color  = 'red';
export default function (num1, num2) {
    return num1 + num2;
}
import sum, {color} from './model-1.js'

```

<br />


-------

#### 重新导出一个绑定
```js
import { sum } from './model-1.js';
export { sum }
// 上面的语句可以换成下面的，只通过一条语句也能执行
export { sum } from './model-1.js'
export { sum as add } from './model-1.js'
```

