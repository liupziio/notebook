# 一、点击哪个li哪个加上class类

```js
<style>
    .active {
      color: red;
    }
  </style>

<div id="app">
    <ul>

     //movies赋值给item,index是索引
      <li v-for="item,index in movies" 
         :class="{active : isActive===index}"
         @click="Bth(index)"> 
        {{index}}-{{item}}</li>
        <!--  -->

    </ul>
  </div>

  <script>
    const app = new Vue({
      el: '#app',
      data: {
        movies: ['海王', '海尔兄弟', '火影忍者', '进击的巨人'],
        isActive:0
      },
      methods: {
          Bth(index){
              this.isActive=index
          }
      }
    })
  </script>
```

## 文本说明

+ 注意动态绑定类那里是花括号
  + 

+ 把movies数组中的数据遍历给,item,并且index获取到数组中数据的索引值
+ 定义一个类active为红色,并且动态绑定
+ 绑定动态类时让它 : isActive，而变量初始值为0，这个isActive让他===index（数组中的索引），如果isActive===index，那么就为true，动态绑定的类生效
+ 绑定一个@click事件并且给他传一个参数index（数组中的索引）点击时这个Vue中的isActive=index
+ 



# 二、利用if判断来切换输入框的类型

```js
    <div id="app">
        <span v-if="user">
            <label for="username">用户账号</label>
            <input type="tel" id="username" placeholder="用户账号" key="username">
						<!-- 如果不想input继承上一个input输入的内容，那么就该他加上key=""加上key区分 -->
        </span>

        <span v-else>
            <label for="email">用户邮箱</label>
            <input type="email" id="email" placeholder="用户邮箱" key="email">
        </span>
        <button @click="Bth">切换登录方式</button>
    </div>

<script>
    const app = new Vue({
        el:'#app',
        data:{
            user:true
        },
				methods:{
					Bth(){
						this.user=!this.user
					}
				}
    })
</script>
```



## 文本说明

+ 主要思想：
  + 用 v-if 给一个条件，然后 v-else 否则 
  + 利用按钮函数来改变  if  判断条件的 true 和 false （取反）
+ 知识补充
  + 在切换时如果不想上一个 input 框的输入内容被下一个 input 读取到时
    + 那么给这两个切换的 input 各自加一个 key 而值为不同的两个
  + label 标签中加入 for 属性和 input中 的id一致时点击 label 就是点击 input 框

```js
<label for="username">用户账号</label>
<input type="tel" id="username" placeholder="用户账号" key="username">
```



# 三、购物车案例

### 1.结合v-for,v-if,

### 2.限制最小数,过滤属性,

+ v-bind:disabled="item.count <= 1"  限制这个数不能小于1 

+ HTML代码

```js
	<div id="app">
		<div v-if="books.length">
			<table>
				<thead>
					<tr>
						<td></td>
						<td>书籍名称</td>
						<td>出版日期</td>
						<td>价格</td>
						<td>购买数量</td>
						<td>操作</td>
					</tr>
				</thead>
				<tbody>
					<tr v-for="(item,index) in books">
						<td>{{item.id}}</td>
						<td>{{item.name}}</td>
						<td>{{item.data}}</td>
						<td>{{item.price | showPrice}}</td>
						<td>
							<button @click="minus(index)" v-bind:disabled="item.count <= 1">-</button>
							<!-- v-bind:disabled="item.count <= 1"  限制这个数不能小于1 -->
							{{item.count}}
							<button @click="add(index)">+</button>
						</td>
						<td><button @click="remove(index)">移除</button></td>
					</tr>
				</tbody>
			</table>
			<h2>总价格:{{sum | showPrice}}</h2>
		</div>
		<h2 v-else>购物车是空的</h2>
	</div>

```



+ Vue代码

```js
const app = new Vue({
  el: '#app',
  data: {
    books: [
      {
        id: 1,
        name: '《算法导论》',
        date: '2006-9',
        price: 85.00,
        count: 1
      },
      {
        id: 2,
        name: '《UNIX编程艺术》',
        date: '2006-2',
        price: 59.00,
        count: 1
      },
      {
        id: 3,
        name: '《编程珠玑》',
        date: '2008-10',
        price: 39.00,
        count: 1
      },
      {
        id: 4,
        name: '《代码大全》',
        date: '2006-3',
        price: 128.00,
        count: 1
      },
    ]
  },
  methods: {
    add(index) {//加
      this.books[index].count++
    },
    minus(index) {//减
      this.books[index].count--
    },
    remove(index) {//移除
      this.books.splice(index, 1)
    }
  },
  computed: {

    sum() {//计算全部价格
      let number = 0
      for (let i = 0; i < this.books.length; i++) {
        number += this.books[i].price * this.books[i].count
      }
      return number
    }
  },
  filters: {//过滤器属性
    showPrice(price) {//过滤到这个price时候
      return '¥' + price.toFixed(2)
      //返回 ￥ + price和保留两位小时
    }
  }
})
```



# 四、父子组件通信结合案例

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
</head>
<body>

<div id="app">
  <cpn :number1="num1"
       :number2="num2"
       @num1change="num1change"
       @num2change="num2change"/>
</div>

<template id="cpn">
  <div>
    <h2>props:{{number1}}</h2>
    <!-- 父组件传下来的，子组件命名 -->
    <h2>data:{{dnumber1}}</h2>
    <!-- 父组件传下来的，子组件命名 -->

    <!--<input type="text" v-model="dnumber1">-->
    <input type="text" :value="dnumber1" @input="num1Input">
    <!-- 动态绑定子组件中的dnumber1并且dnumber1已经跟父组件传过来的相等了 @input是监听input变化调用这个函数num1Input -->
    <h2>props:{{number2}}</h2>
    <h2>data:{{dnumber2}}</h2>
    <!--<input type="text" v-model="dnumber2">-->
    <input type="text" :value="dnumber2" @input="num2Input">
    <!-- 动态绑定子组件中的dnumber2并且dnumber2已经跟父组件传过来的相等了 @input是监听input变化调用这个函数num2Input -->
  </div>
</template>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      num1: 1,
      num2: 0
    },
    methods: {
      num1change(value) { //父组件定义一个函数(子组件传递的参数)
        this.num1 = parseFloat(value)//让父组件的num1=子组件传递的参数
      },
      num2change(value) {
        this.num2 = parseFloat(value)
      }
    },
    // 子组件
    components: {
      cpn: {
        template: '#cpn',
        props: {//父组件传给子组件,子组件读取
          number1: Number,
          number2: Number
        },
        data() {//子组件自己的变量===传过来的变量
          return {
            dnumber1: this.number1,
            dnumber2: this.number2
          }
        },
        methods: {
          num1Input(event) {
            // 1.将input中的value赋值到dnumber中
            this.dnumber1 = event.target.value;

            // 2.为了让父组件可以修改值, 发出一个事件
            this.$emit('num1change', this.dnumber1)

            // 3.同时修饰dnumber2的值
            this.dnumber2 = this.dnumber1 * 100;
            this.$emit('num2change', this.dnumber2);
          },
          num2Input(event) {
            this.dnumber2 = event.target.value;
            this.$emit('num2change', this.dnumber2)

            // 同时修饰dnumber2的值
            this.dnumber1 = this.dnumber2 / 100;
            this.$emit('num1change', this.dnumber1);
          }
        }
      }
    }
  })
</script>

</body>
</html>
```

