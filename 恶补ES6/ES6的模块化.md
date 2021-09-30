# ES6模块化导入与导出

## 模块导出export{}

+ index.html页面

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>

<!-- 需要script标签类型===module时候才能使用 ES6 的模块导出导入 -->
<script src="./aaa.js" type="module"></script>
<script src="./bbb.js" type="module"></script>
<script src="./mmm.js" type="module"></script>
</body>
</html>
```



+ 导出aaa.js

```js
var name = '小明'
var age = 18
var flag = true

function sum(num1, num2) {
  return num1 + num2
}

if (flag) {
  console.log(sum(20, 30));
}

// 1.导出方式一:
//定义之后导出
export {
  flag, sum
}

// 2.导出方式二:
//定义时候直接导出
export var num1 = 1000;
export var height = 1.88


// 3.导出函数/类
export function mul(num1, num2) {
  return num1 * num2
}

//ES6导出类,类里边是函数
export class Person {
  run() {
    console.log('在奔跑');
  }
}

// 5.export default
// const address = '北京市'
// export {
//   address
// }
// export const address = '北京市'
// const address = '北京市'
//  
//  默认导出的address,导入者可以改名字    (默认导出只能导出一个)
// export default address

//  默认导出的function,导入者可以改随便命名    (默认导出只能导出一个)
export default function (argument) {
  console.log(argument);
}
```





## 模块导入import  {}  from  "";

+ mmm.js导入

```js
// 1.导入的{}中定义的变量
import {flag, sum} from "./aaa.js";

if (flag) {
  console.log('小明是天才, 哈哈哈');
  console.log(sum(20, 30));
}

// 2.直接导入export定义的变量
import {num1, height} from "./aaa.js";

console.log(num1);
console.log(height);

// 3.导入 export的function/class
import {mul, Person} from "./aaa.js";

console.log(mul(30, 50));

const p = new Person();
p.run()

// 4.导入 export default中的内容
import addr from "./aaa.js";

addr('你好啊');

// 5.统一全部导入
// import {flag, num, num1, height, Person, mul, sum} from "./aaa.js";
//导入 全部 名字 是aaa 来自 './aaa.js'
import * as aaa from './aaa.js'

console.log(aaa.flag);
console.log(aaa.height);


```



+ 导入bbb.js

```js
import {sum} from './aaa.js'

var name = '小红'
var flag = false

console.log(sum(100, 200));


```



# 文本说明

## 注意点

+ 如果需要引入script并且script有模板导入导出
  + 那么需要把**script**标签类型改为**module**
    + 不然不可以使用模块化
+ 导出函数时，不需要加上括号，即便是有参数也不需要
  + 导入调用时候传参数就可以
    + 不然是一个空的函数