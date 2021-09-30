# 动态控制属性

## v-bind:||:基础使用

### 	实例

#### 			作用

+ 动态绑定，
  + 使用场景
    + 哪个属性需要动态绑定，哪个属性前边加上v-bind

```js

<img v-bind:src="imgURL" alt="">
    #语法糖
<a :href="aHref">百度一下</a>

 data: {
      message: '你好啊',
      imgURL: 'https://img11.360buyimg.com/mobilecms/s350x250_jfs/t1/20559/1/1424/73138/5c125595E3cbaa3c8/74fc2f84e53a9c23.jpg!q90!cc_350x250.webp',
      aHref: 'http://www.baidu.com'
    }
```



## 动态控制类（对象语法）

### 语法

+ :class="{ key (calss)	：布尔值}"

#### 实例

```js
 <h2 class="title" v-bind:class="{active: isActive, line: isLine}">{{message}}</h2>
	//	:calss动态控制class line和active都是动态添加的类
  <h2 class="title" v-bind:class="getClasses()">{{message}}</h2>
	// 	
  <button v-on:click="btnClick">按钮</button>

  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      isActive: true, //真假
      isLine: true    //真假
    },
    methods: {
      btnClick: function () {
        this.isActive = !this.isActive
        //这个的isActive = 这个的isActive取反
      },
      getClasses: function () {
        return {active: this.isActive, line: this.isLine}
        //返回 active=this.isAction,line = this.isLine
      }
    }
  })
```



## 动态控制类(数组语法)

### 实例

```js
 <h2 class="title" :class="[active, line]">{{message}}</h2>
//这里的active类=aaa
//line类=bbb
  <h2 class="title" :class="getClasses()">{{message}}</h2>
//这个函数返回active,line 也就是aaa,bbb


 const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      active: 'aaa',
      line: 'bbb'
    },
    methods: {
      getClasses: function () {
        return [this.active, this.line]
      }
    },
    
  })
```



## 动态控制属性(style)	(对象语法)

### 语法

+ :style="{ key(属性名color...)	:	value(属性值' red...' ) }"
+ 如果不把属性值做成一个变量，那么这里属性值记得用 ‘ ’ 圈起来要不然系统会以为是变量

#### 实例

```js
<!-- 第一种方法偏长 -->
  <h2 :style="{fontSize: finalSize + 'px', backgroundColor: finalColor}">{{message}}</h2>
  <!-- 第二种封装 -->
  <h2 :style="getStyles()">{{message}}</h2>
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      finalSize: 100,
      finalColor: 'red',
    },
    methods: {
      getStyles: function () {
        return {fontSize: this.finalSize + 'px', backgroundColor: this.finalColor}
      }
    }
  })
</script>
```

## 动态控制属性(style)	(数组语法)

### 语法

+ ：style “【变量1，变量2】”
+ 变量1：{backgroundColor: 'red'},
+ 变量2： {fontSize: '100px'},

```js
//第一种方法数组展示，偏长
<div id="app">
  <h2 :style="[baseStyle, baseStyle1]">{{message}}</h2>
//第二种方法封装展示
<h2 :style="style()">{{message}}</h2>
</div>

const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      baseStyle: {backgroundColor: 'red'},
      baseStyle1: {fontSize: '100px'},
    },
    methods: {
      style(){
        return [this.baseStyle,this.baseStyle1]
      }
  })
```















# 插值操作



## V-for	循环遍历

### 实例

```js
<div id="app">
    <ul>
        <li v-for="item in movies">{{item}}</li>
	//把movies中的数据遍历给item,之后每一个item === movies中的每一个数据
		//li中加入v-for循环数据到li中
    </ul>
</div>

<script src="../js/vue.js"></script>
<script>
    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊',
            movies: ['星际穿越', '大话西游', '少年派', '盗梦空间']
        }
    })
</script>
```



## v-on：|| @	绑定事件

### 实例

```js
#v-on:
<button v-on:click="sub">-</button>
#@	//俗称语法糖
<button @click="sub">-</button>
```



## v-once	移除响应式

### 实例

```js
#这里的h2继续响应式
<h2>{{message}}</h2>
#这里的h2移除响应式
<h2 v-once>{{message}}</h2>
```



## v-html	返回html或文本

### 实例

#### 	作用

+ 可以将传进来的数据转化成HTML

```js
<div id="app">
  <h2>{{url}}</h2>	//这里只能返回<a href="h...>百度一下</a>
  <h2 v-html="url"></h2> //这里会返回html可以点击的a标签
</div>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊',
      url: '<a href="http://www.baidu.com">百度一下</a>'
    }
  })
</script>
```



## v-text	返回文本	

### 实例

#### 	作用

+ 单纯返回数据中的文本
  + 缺点：
    + 会把html中的文本覆盖

```js
<h2 v-text="message">, 李银河!</h2>
//返回	你好啊 会把以前文本覆盖
 data: {
      message: '你好啊'
    }
```



## v-pre	获取不解析的内容	

### 实例

#### 	作用

+ 不解析内容直接返回

```js
<h2 v-pre>{{message}}</h2>
//返回	{{message}}
  data: {
      message: '你好啊'
    }
```



## v-cloak	防止页面闪动

### 实例

#### 	作用

+ 防止进入页面时候，一些资源没有加载完，客户看到源码

```js
 <style>
    [v-cloak] {
      display: none;
    }
  </style>

<div id="app" v-cloak>
  <h2>{{message}}</h2>
</div>

<script>
  // 在vue解析之前, div中有一个属性v-cloak
  // 在vue解析之后, div中没有一个属性v-cloak
      
  setTimeout(function () {	
      ###延迟一秒解析,解析之后v-cloak自动就没了
    const app = new Vue({
      el: '#app',
      data: {
        message: '你好啊'
      }
    })
  }, 1000)
</script>
```

