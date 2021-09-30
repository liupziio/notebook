# 变量赋值

**var**

重复声明，不能限制修改，函数级

**let**

防止重复声明，变量，块级作用域

## let实例

```js
#原生js闭包实现，点击那个弹出第几个
  for (var i=0; i<btns.length; i++) {
    (function (i) { // 0
      btns[i].addEventListener('click', function () {
        console.log('第' + i + '个按钮被点击');
      })
    })(i)
  }//闭包原理是调用一下参数,function本身是一个块级作用域

#let实现，点击那个弹出第几个
const btns = document.getElementsByTagName('button')
  
  for (let i = 0; i < btns.length; i++) {
    btns[i].addEventListener('click', function () {
      console.log('第' + i + '个按钮被点击');
    })
  }//这是用let定义i本身就是块级作用域所以用的都是它自己的i
```



**const**

防止重复声明，常量，块级作用域

+ 注意点
  + 不可以const aa，然后以后再去调用
  + 不能改值,但是可以改属性

## const实例

```js
const obj = {
    name: 'why',
    age: 18,
    height: 1.88
  }
  obj.name = 'kobe';
  obj.age = 40;
  obj.height = 1.87;//const常量里边的属性是可以改的

console.log(obj)
//返回结果【name = 'kobe',age = 40,obj.height = 1.87;】
```



# 解构赋值

## 注意点

1.两边结构一致

```javascript
  let{a,b} = {a:12,b:15}
        console.log(a,b)
       		 //12,15
  let[a,b] = [5,8]
 		 console.log(a,b)
			//5,8
  arr = [11,12,13]
        let[a,b] = arr
        console.log(a,b)
        //11 12
let{a,b} = [5,8]
	console.log(a,b)
		//报错,原因左右结构不同

```

2.右边必须是一个东西

3.赋值解构必须同时完成



