# 1、push()	在最后面添加元素

```js
this.letters.push('aaa')
	//添加几个参数那么就在最后边添加几个元素
this.letters.push('aaaa', 'bbbb', 'cccc')
```



# 2、unshift()  在最前面添加元素

```js
this.letters.unshift()
	//添加几个参数那么就在最前边添加几个元素
this.letters.unshift('aaa', 'bbb', 'ccc')
```



# 3、pop() 删除最后一个元素

```js
this.letters.pop();
```



# 4、shift() 删除第一个元素

```js
this.letters.shift();
```





# 5、splice() 删除元素，替换元素，插入元素

```js
//  第一个参数都是从哪里开始
        // 删除元素: 第二个参数传入你要删除几个元素(如果没有传,就删除后面所有的元素)
        // 替换元素: 第二个参数, 表示我们要替换几个元素, 后面是用于替换前面的元素,传多少都可以
        // 插入元素: 第二个参数, 传入0, 并且后面跟上要插入的元素
 this.letters.splice(1, 3, 'm', 'n', 'l', 'x')
//从第一个开始，替换三个，替换上后边这 4 个
 this.letters.splice(1, 0, 'x', 'y', 'z')
//从第一个开始，插入这三个元素
```



# 6、sort() 数组排序

```js
this.letters.sort()
```



# 7、reverse() 数组反转

```js
this.letters.reverse()
```



# 二、Vue.set()修改数组中的某一个

+ 响应式

```js
        // set(要修改的对象, 索引值, 修改后的值)
	Vue.set(this.letters, 0, 'bbbbbb')
	//// set(要修改的对象, 字符串,字符串等于什么 )
Vue.set(state.info,'address','洛杉矶')
```



