# 注意点

+ html页面手机低版本不支持

```js
#es6转es5
<script type="text/javascript" src="./js/browser.min.js"></script>
<script type="text/javascript" src="./js/polyfill.min.js"></script>
#.........
<script lang = babel>
```







## 1、数据的前后变化



```js
$watch
vm.watch('a',function(newVal,oldVal){
    console.log(newVal,oldVal)
    //查询a属性的前后变化
})
```

## 2、路由的重定向

```js
{//当路径为空时,重定向去home路径
            path:"",
            redirect: '/home'
        },
```

## 3、利用路由name携带参数

```js
routes: [
    {
      path: '/son',
      name: 'son',
      component: SonComponent
      //component: resolve => require(['../components/tab-bar/component/son/SonComponent.vue'], resolve)
    }
]

// vue页面中
this.$router.push({name: 'son',  params: {pa: aa})

// 接收页面
console.log(this.$route.params.pa)
```

## 4、设置最低值

```js
<button @click="minus(index)" :disabled="item.count <= 0">-</button>
```



## 5、 v-loading加载

```js
//全局loading
<template>
    <div v-loading="loading"> </div>
</template>

在data 中定义初始化， loading: false，同时在mounted()中将 this.loading设置为true,再去请求接口

在接口的回调函数中，将 this.loading 设为false，到达效果。

//局部loading
<template>
    <div> 
        <section v-loading="loading"></section>
    </div>
</template>
```



# 一、Vue路由



## 1.嵌套路由(局部)

```js
 #配置路由
 // redirect: '/gongwentg/fslist',
//设置路由重定向,进入路由显示哪一页,
 #因为是局部切换所以页面在/gongwentg页面中显示/gongwentg/fslist页面
 #(只是局部切换的页面)
{
    path: '/gongwentg',
    name: 'gongwentg',
    component: () => import('pages/homelink/gongwentg.vue'),
    redirect: '/gongwentg/fslist',
    children: [
      { path: 'fslist', component: () => import('pages/homelink/gwtg_child/fabu.vue') },
      { path: 'jieshou', component: () => import('pages/homelink/gwtg_child/jieshou.vue') }
    ]
  },

#页面使用
//DOM中路由显示位置
<router-view></router-view>

 changeView(val) {//方法中切换路由
      if (val == "1") {
        this.$router.replace("/gongwentg/fslist");
      } else {
        this.$router.replace("/gongwentg/jieshou");
      }
  },
```



## 2.监听当前活跃路由



```js

watch: {
    $route:{
      handler(newName,oldName){
        console.log(newName);
        console.log(oldName);
      },
      immediate:true//这里加上 immediate 第一次赋值就会去执行handler函数
    }
  },
```



## 3.keep-alive



+ 使用 **keep-alive** 来保存当前页面状态

```js
//这两个活跃与不活跃要和keep-alive一起用不然无效
    activated() {//处于活跃状态(使用暂存)
       console.log('Home activated活跃的')
    },
    deactivated() {//处于不活跃状态(暂存)
       console.log('Home deactivated 不活跃的')
    },
```



+ 属性
  - `include` - 字符串或正则表达式。只有名称匹配的组件会被缓存。
  - `exclude` - 字符串或正则表达式。任何名称匹配的组件都不会被缓存。
    - `exclude` 的优先值 大于 `include`
  - `max` - 数字。最多可以缓存多少组件实例。



```js
<!-- 逗号分隔字符串 -->
<keep-alive include="a,b">
  <component :is="view"></component>
</keep-alive>
<!-- 正则表达式 (使用 `v-bind`) -->
<keep-alive :include="/a|b/">
  <component :is="view"></component>
</keep-alive>
<!-- 数组 (使用 `v-bind`) -->
<keep-alive :include="['a', 'b']">
  <component :is="view"></component>
</keep-alive>
```





```js

####max的使用
//:max="3" 最多可以缓存多少组件实例。一旦这个数字达到了，在新实例被创建之前，已缓存组件中最久没有被访问的实例会被销毁掉。
<keep-alive include="name" >
  <view></view>
</keep-alive>

```



### 1、碰到的问题

#### 一、切换页面时来判断 当前页面(缓存/刷新)

+ **例：当前有三个页面分别是 首页、列表页、详情页**
  + **需求：列表页>首页>列表页 ** 列表页最初始状态
  +  **列表页>详情页>列表页** 列表页缓存进入详情页之前的状态





+ 一、单页缓存时使用下边方法

```js
<keep-alive>
    <router-view v-if="$route.meta.keepAlive"></router-view>
</keep-alive>
<router-view v-if="!$route.meta.keepAlive"></router-view>
```

+ 上边的方法 **列表页>详情页>列表页** 列表页会缓存
+ 但是  **列表页>首页>列表页** 列表页不是最初始的状态





+ 二、使用下边的方法



1. 在入口app页面

```js
#在app页面
      <keep-alive :include="keepAlive">//这里keepAlive设置成动态的
        <router-view />
      </keep-alive>

computed: {
    //将监听到的keepAlive属性，动态穿给keep-alive组件
    keepAlive() {
      return this.$store.getters.keepAlive;
    }
  }
```



2. 在首页

```js
#在首页 去列表的方法中
 this.$store.commit("setKeepAlive", ["列表页"]);
```



3. 在列表页

```js
  beforeRouteEnter(to, from, next) {
    next(vm => {
      //判断是否从（详情页）进入，如果是，那么仍需将（列表）缓存
      if (from.name === "详情") {
        vm.$store.commit("setKeepAlive", ["xinwenzx"]);
      }
    });
  },
  beforeRouteLeave(to, from, next) {
    //判断将要去的页面是否为（详情页），若是，则需要将（列表页）缓存
    if (to.name === "详情页") {
      this.$store.commit("setKeepAlive", ["列表页"]);
    } else {
      //否则将缓存队列清空，（这里只缓存了一个所以直接清空了，如果多个可以在 store 中多定义两个，或者在数组做判断）
      this.$store.commit("setKeepAlive", []);
    }
    next();
  }
```



4. 在 **vuex** 中

```js
	state: {
        keepAlive: [''],
    },
    mutations: {
        //这里做更新
        setKeepAlive(state, keepAlive) {
            state.keepAlive = keepAlive
        }
    },
    getters: {
        //这里计算属性keepAlive = state.keepAlive（其实有点多此一举,可以在直接调用state中的keepAlive，但是我不想改了）
        keepAlive: state => {
            return state.keepAlive
        },
    }
```



+ 以上做完就可以完成需求

  **列表页>首页>列表页 ** 列表页最初始状态

  **列表页>详情页>列表页** 列表页缓存进入详情页之前的状态







# 二、计算属性和监听



1.  **computed** 和 **watch** 搭配使用

```js
 // 计算属性来存储vuex的数据,不然监听变化，监听不到
  computed: {
    getIndex() {
      return this.$store.state.page;
    }
  },
  // 这里边直接监听计算属性的函数
  watch: {
    getIndex(val) {
     console.log(val);//变化时打印
    }
  },
```



2. **watch** 其他属性

+ watch有一个特点，就是当值第一次绑定的时候，不会执行监听函数，只有值发生改变才会执行。

+ ### immediate和handler

  + **immediate** 如果为 **true** 那么就会去监听到第一次的绑定

```js
new Vue({
  el: '#root',
  data: {
    cityName: ''
  },
  watch: {
    cityName: {
    　　handler(newName, oldName) {
      　　// ...
    　　},
    　　immediate: true//这里加上 immediate 进入页面就会去执行handler函数
    },
       qrcodetext: {
      handler(newVal) {
        console.log(newVal);
      },
      deep: true,
    },
  } 
     
})
```



+ **deep** **深度监听**

```js
new Vue({
  el: '#root',
  data: {
    cityName: {id: 1, name: 'shanghai'}
  },
  watch: {
    cityName: {
      handler(newName, oldName) {
      // ...
    },
        deep: true,//这里加入deep那么 cityName 对象中的值变化时也会执行 handler 函数
        immediate: true
    }
  } 
})
```

+ 如果只想监听对象中的其中一个属性那么可以只去监听其中的某个属性

```js
watch: {
    'cityName.name': {
      handler(newName, oldName) {
      // ...
      },
      deep: true,
      immediate: true
    }
  }
```





# 三、Vue内置API方法

