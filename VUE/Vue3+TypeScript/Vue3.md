# vue源码

## 1、三大核心系统

+ **Compiler模块** : 编译模板系统
+ **Runtime模块**：也可以称之为Renderer模块，真正的渲染模块；
+ **Reactivity模块**：响应式系统





# 一、组件

## 1、异步组件



**defineAsyncComponent vue异步组件API**

**问：**  异步组件的应用场景与作用 ？

**答：**

+ 异步组件可以让 Vue 第一次渲染时更加快一点
+ 对于Webpack 来说 项目打包时，会将这个异步组件打包成一个单独的 js  当使用到时，再去加载这个 js 文件。

**使用方法**



```vue
<template>
  <div>
    App组件
    <AsyncCategory></AsyncCategory>
  </div>
</template>

<script>
import { defineAsyncComponent } from "vue";
import Loading from "./loading.vue"
// 工厂函数
// const AsyncCategory = defineAsyncComponent(() => import("./AsnycCategory.vue"));//简写
   
//对象方式
const AsyncCategory = defineAsyncComponent({
    loader:()=>import("./AsnycCategory.vue"),
    loadingComponent:Loading,//没有加载出来站位
    // errorComponent:'',//组件加载失败显示的组件
    delay:2000,//在显示loading组件之前,等待多长时间(延迟显示)
   /**
   *
   * @param {*} error 错误信息对象
   * @param {*} retry 一个函数，用于指示当 promise 加载器 reject 时，加载器是否应该重试
   * @param {*} fail  一个函数，指示加载程序结束退出
   * @param {*} attempts 允许的最大重试次数
   */
   onError:function(error, retry, fail, attempts){
     if (error.message.match(/fetch/) && attempts <= 3) {
      // 请求发生错误时重试，最多可尝试 3 次
      retry()
    } else {
      // 注意，retry/fail 就像 promise 的 resolve/reject 一样：
      // 必须调用其中一个才能继续错误处理。
      fail()
    }
}
});

export default {
  components: {
    AsyncCategory,
  },
};
</script>
```



## 2、Suspense插槽 处理组件不显示

**Suspense vue试验性API 随时修改**

**问：**Suspense 的应用场景与作用 ？

**答：**

+ 可以处理组件如果没有加载出来去显示另一个



**使用方法 (异步组件为例)**

```vue
<template>
  <suspense>
    <template #default> <!-- 默认显示 -->
      <todo-list />
    </template>
    <template #fallback> <!-- 没有加载到,显示 -->
      <div>
        Loading.... <!-- 这里也可以放组件 -->
      </div>
    </template>
  </suspense>
</template>

<script>
   import { defineAsyncComponent } from "vue";//异步组件API
export default {
  components: {
    TodoList: defineAsyncComponent(() => import('./TodoList.vue'))
  }
}
</script>

```



## 3、组件之间的v-model

**问：**组件之间的v-model 的应用场景与作用 ？

**答：**

+ 应用场景多了去了 , 作用大了去了 , 封装个组件不要双向绑定嘛, **擦**



**使用方法 ( 利用v-model标签上隐性绑定的update:name方法 )**

+ **父组件**

```vue

<template>
  <div>
    <h2>{{ message }}</h2>
     <h2>{{ title }}</h2>

    <hy-input v-model="message" v-model:title="title"></hy-input>
          <!-- 这里默认会绑定 update:modelValue update:title 两个事件等同于下边的举例-->
     <!--    <hy-input v-model="message" v-model:title="title" @update:modelValue="message=$event" @update:title="title=$event"></hy-input> -->
      

     
  </div>
</template>

<script>
import HyInput from "./HyInput.vue"
export default {
    components:{
        HyInput
    },
  data() {
    return {
      message: "lpz",
      title:'哈哈哈'
    };
  },
};
</script>

<style scoped>
</style>


```



+ **子组件**

```vue
#子组件
<template>
  <div>
    <h2>我是传进来的：{{ modelValue }}</h2>
    <input v-model="value" />
    <input v-model="title1" />
  </div>
</template>

<script>
export default {
  props: {
    modelValue: String,
    title: String,
  },
  emits: ["update:modelValue", "update:title"],//注册自定义事件
  computed: {//利用computed显示(get)与调用自定义事件(set)
    value: {
      set(value) {
        this.$emit("update:modelValue", value);
      },
      get() {
        return this.modelValue;
      },
    },
    title1: {
      set(value) {
        this.$emit("update:title", value);
      },
      get() {
        return this.title;
      },
    },
  },
};
</script>

<style scoped>
</style>
```





# 二、插槽





# 三、基础Api

## 1、customRef（自定义ref）

+ 自定义ref防抖事件

**customRef 有两个参数，并且返回一个对象，对象中必须有set与get函数**

+   track 搜集依赖
+ trigger 触发更新

```js
import { customRef } from "vue";
// 自定义ref
export default function(value) {
  let timer = null;
  // track 搜集依赖
  // trigger 触发更新
  return customRef((track, trigger) => {
    return {
      get() {
        track();
        return value;
      },
      set(newValue) {//延迟一秒更新数据
        clearTimeout(timer);
        timer = setTimeout(() => {
          value = newValue;
          trigger();
        }, 1000);
      },
    };
  });
}
//使用
import debounceRef from "./hook/useDebounceRef.js"
setup() {
    const message = debounceRef("Hello World");
    return {
      message,
    };
  },
```



## 2、computed使用



**computed本身返回的是一个ref对象**

+ 实例

```js
<h2>{{ fullName }}</h2>
    <button @click="changeName">修改firstName</button>

import { ref, computed } from "vue";
setup() {
    const fristName = ref("Kobe");
    const lastName = ref("Bryant");
    //1.直接返回值
    // const fullName = computed(() => fristName.value + " " + lastName.value);
    //2.传入对象设置set，get
    const fullName = computed({
      get: () => fristName.value + " " + lastName.value,
      set(newValue) {
        const names = newValue.split(" ");
        fristName.value = names[0];
        lastName.value = names[1];
        console.log(newValue);
      },
    });

    const changeName = () => {
      //   fristName.value = "James";
      fullName.value = "code why";
    };
    return {
      fullName,
      changeName,
    };
  },
```



## 3、watch的使用

### 两种监听模式

#### 1. watchEffect 自动搜集响应式依赖

**弊端：**

第一次一定会执行，因为会去查找内部有些哪些需要监听的值

+ 当前函数会在最开始立即执行一次，并且在立即执行的同时会去查找函数内使用了哪些值，并监听他们



**使用:**

```js
 <div>name-{{ name }}</div>
    <div>age-{{ age }}</div>
    <button @click="changeName">nameChange</button>
    <button @click="changeAge">AgeChange</button>


import { ref, watchEffect } from "vue";
export default {
  setup() {
    const name = ref("why");
    const age = ref(18);
    const changeName = () => (name.value = "kobe");
    const changeAge = () => age.value++;
    watchEffect(() => {
      console.log(
        "watchEffect-changeName",
        name.value,
        "watchEffect-changeAge",
        age.value
      );
    });
    return {
      name,
      age,
      changeName,
      changeAge,
    };
  },
};
```



##### watchEffect 的停止侦听

+ watchEffect 返回的是一个函数,调用即可停止监听

**使用：**

```js
 const shop =   watchEffect(() => {
      console.log(
        "watchEffect-changeName",
        name.value,
        "watchEffect-changeAge",
        age.value
      );
    });
     const changeAge = () => {
       age.value++;
       if(age.value>25){
         shop()
       }
     }
```

##### 清除watchEffect副作用

**什么是副作用：**

例：监听一个值的变化来发送网络请求，多次变化上一次数据没有回来就发送了第二个请求，这个过程就叫 `watchEffect副作用` 



**使用：**

1. 可以用wacthEffect返回值清空所有
2. 也可以根据情况自己封装

```js
  const shop = watchEffect((test) => {
      // 根据name和age两个变量发送网络请求
      const timer = setTimeout(() => {
        console.log("模拟网络请求");
      }, 2000);
      test(() => {
         //只要是组件销毁便会执行
        // 在这里清楚无用的副作用
        clearTimeout(timer);
      });
      console.log(
        "watchEffect-changeName",
        name.value,
        "watchEffect-changeAge",
        age.value
      );
    });
    const changeAge = () => {
      age.value++;
      if (age.value > 25) {
        shop();
      }
    };
```



##### watchEffect 第二个参数

+ 第二个参数是来控制 watchEffect 的立即监听

**例子：**

```js
  const title = ref(null);
    watchEffect(()=>{
      console.log(title.value);
    },{
      flush:"post"
      // flush:'post'

      // // flush:"sync"

    })
    return {
     title,
    };
```



#### 2. watch 指定侦听

+ watch 的参数
  + 第一个参数为监听的对象
    + 可多个侦听，传入数组
  + 第二个参数为回调函数
  + 第三个参数为配置
    + `deep` 深度侦听
    + `immediate` 立即执行

```js
  // 1.定义可响应对象
    const info = reactive({
      name: "why",
      age: 18,
      friend: {
        name: "kobe",
      },
    });

    // 2.侦听器watch
    watch(()=>({...info}), (newValue, oldValue) => {
      console.log("newValue:", newValue, "oldValue:", oldValue);
    },{
      deep:true,//深度侦听
      immediate:true//立即执行
    });

    const changeInfo = () => {
      info.friend.name = "lpz";
    };
```





## 4、在setup中使用ref

+ 在`setup`中定义一个`ref`对象
+ 并设置给行内元素的`ref`即可

**示例**

```js
 <h2 ref="title">哈哈哈</h2>

import { ref, watchEffect } from "vue";

 setup() {
    const title = ref(null);
    watchEffect(()=>{
      console.log(title.value);
    },{
      flush:"post"//第一次不监听/不然第一次是null
    })
    return {
     title,
    };
  },
```





## 5、render函数与h函数



**render函数为渲染函数，使用render时不需要template模板**

**h函数为渲染每一个节点函数，并且有三个参数**

+ 第一个参数为节点名称(`必须`) 例如 ： div h2 span
+ 第二个参数为节点的属性(`可选官方建议如果没有就传null`)，例如class、点击事件、属性
+ 第三个参数为子节点(`可选`) 可嵌套



**实例：render与h函数的基本使用**

```js
import {  h } from 'vue'

export default {
   render(){
       return h("h2",{class:"title"},"Hello Render")
   }
}
```

**实例：实现计数器（也可以放在setup返回值,setup返回一个函数）**

```js
 setup() {
    const counter = ref(0);
    // return {
    //   counter,
    // };
    return ()=>{
        return h("div", { class: "app" }, [
      h("h2", null, `当前计数：${counter.value}`),
      h(
        "button",
        {
          onClick: () => counter.value++,
        },
        "+1"
      ),
      h(
        "button",
        {
          onClick: () => counter.value--,
        },
        "-1"
      ),
    ]);
    }
  },
//   render() {
//     return h("div", { class: "app" }, [
//       h("h2", null, `当前计数：${this.counter}`),
//       h(
//         "button",
//         {
//           onClick: () => this.counter++,
//         },
//         "+1"
//       ),
//       h(
//         "button",
//         {
//           onClick: () => this.counter--,
//         },
//         "-1"
//       ),
//     ]);
//   },
```

**实例：使用插槽**

+ App.vue

```js
import { h, ref } from "vue";
import HelloWorld from "./HelloWorld.vue";

export default {
  render() {
    return h(HelloWorld, null, {
      default: (props) =>
        h("span", null, `我是传入的插槽 插槽的参数${props.name}`),//props中装载着传过来的值
    });
  },
};
```

+ HelloWorld.vue

```js

import { h, ref } from "vue";

export default {
  render() {
    return h("div", null, [
      h("h2", null, "Hello World"),
      this.$slots.default
        ? this.$slots.default({ name: "lpz" })//这里可以传值给app.vue
        : h("span", null, "我是HelloWorld的默认值"),//这里收集插槽，如果有名字为default的插槽就使用插槽,否则输出一个span
    ]);
  },
};
```



## 6、directives(自定义指令)



### 1. 基本使用

**说明：**

自定义指令的生命周期中都传入了四个参数

+ 第一个参数：`el`   当前`Dom`元素 
+ 第二个参数为：`bindings` 装载自定义指令的传值与修饰符
  + 其中：value为传入的值
  + modifiers 为修饰符，
+ 第三个参数为虚拟节点 `vnode`
+ 第四个参数为前一个虚拟节点 `preVnode`

##### 局部自定义指令

+ 局部自定义指令设置在每一个单独的组件中
+ 自定义指令,第一个参数为名字,第二个为回调函数

```js
<template>
  <div>
    <button
      v-button.aaa.bbb="'自定义指令传值'"
      v-if="counter < 3"
      @click="increment"
    >
      计数器:{{ counter }}
    </button>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  directives: {
    //局部动态自定义指令
    button: {
      created(el, bindings, vnode, preVnode) {
        // bindings 为自定义指令传值与修饰符的容器
        //value 为传入的数据 
        // modifiers 为修饰符 会为true
        console.log("modifiers");
        console.log("created");
        console.log(bindings);
      },
      beforeMount(el, bindings, vnode, preVnode) {
        console.log("beforeMount");
      },
      mounted(el, bindings, vnode, preVnode) {
        console.log("beforeMount");
      },
      beforeUpdate(el, bindings, vnode, preVnode) {
        console.log("beforeUpdate");
      },
      updated(el, bindings, vnode, preVnode) {
        console.log("updated");
      },
      beforeUnmount(el, bindings, vnode, preVnode) {
        console.log("beforeUnmount");
      },
      unmounted(el, bindings, vnode, preVnode) {
        console.log("unmounted");
      },
    },
  },
  setup() {
    const counter = ref(0);
    const increment = () => {
      counter.value++;
    };
    return {
      counter,
      increment,
    };
  },
};
</script>

```



##### 全局自定义指令

```js
const app = createApp(App);
app.directive("focus", {
  //全局自定义指令,第一个参数为名字,第二个为回调函数
  mounted(el, bindings, vnode, preVnode) {
    el.focus();
  },
});
app.mount("#app");
```

##### 封装全局数据格式化

**可用于需要统一理的数据**

![image-20211007142318140](.\Vue3.assets\image-20211007142318140.png)

<img src="F:\learn\note book\VUE\Vue3+TypeScript\Vue3.assets\image-20211007142318140.png" alt="image-20211007142318140" style="zoom:100%;" />





### 2. 指令的生命周期



![image-20211007130728367](.\Vue3.assets\image-20211007130728367.png)



## 7、teleport（template插入到指定容器中）



**作用：将元素插入到指定容器中**

+ app.vue

```js
  <div>
        <teleport to="#lpz">
            <h2>teleport</h2>
            <span>插入到id为lpz的容器中</span>
        </teleport>
         <teleport to="#lpz">
            <div>追加</div>
        </teleport>
    </div>
```

+ index.html

```js
 <div id="app"></div>
    <div id="lpz"></div>
```

**效果**

![image-20211007145028270](.\Vue3.assets\image-20211007145028270.png)





## 8、全局注册插件(app.use())

**说明：**

全局注册插件

+ 对象形式
  + 会去调用对象中的`install`方法并且传入app实例
+ 函数形式
  + 注册函数插件直接将app传给函数
  + 并且可以使用 全局`mixin`、`component`等事件



**mian.js**

```js
import pluginsObject from "./plugins/plugins_object.js"
import pluginsFuntion from "./plugins/plugins_Funtion.js"

app.use(pluginsObject)//这里注册插件其实直接会调用里边的install方法,并且转入app
app.use(pluginsFuntion)//注册函数插件直接将app传给函数
```

**lugins_object.js**

```js
export default {
  install(app) {
    console.log(app);
    app.config.globalProperties.$name = "lpz";
  },
};

```

**plugins_Funtion.js**

```js
export default function (app) { 
   console.log(app);
 }
```



**在组件中使用全局属性**

+ setup

```js
import {getCurrentInstance} from "vue"//获取组件实例 
setup(props) {
            const instance = getCurrentInstance()//获取组件实例
            console.log(instance.appContext.config.globalProperties.$name)//setup获取全局注册实例属性
        },

```

+ vue2

```js
        mounted() {
            console.log(this.$name)
        },
```

















# 四、Vue中认识jsx

## 1、基本使用

**目前VueCli 4.5.0 已经默认支持jsx**

+ App.vue

```js

<script>
import {ref} from "vue"
import HelloWorld from "./HelloWorld.vue";
export default {
    setup() {
        const counter = ref(0)
        return{
            counter
        }
    },
  render() {
      const increment = ()=>this.counter++
      const decrement = ()=>this.counter--
    return (
       <div>
         <h2>当前计数 {this.counter}</h2>
         <button onClick={increment}>+1</button>
          <button onClick={decrement}>-1</button>
          <HelloWorld>
          {{default:props=><button>我是传入的数据插槽</button>}}
          </HelloWorld>
       </div>
    )
  },
};
</script>

<style scoped>
</style>
```

+ HelloWorld.vue

```js

<script>
export default {
  render() {
    return (
      <div>
        <h2>Hello World</h2>
        {this.$slots.default?this.$slots.default():<span>哈哈哈</span>}
      </div>
    );
  },
};
</script>

<style scoped>
</style>
```







# 五、VueX五大核心

## 1、state



## 2、getters











# 六、TypeScript 与 Vue3



## 1、类型

### 1.1 ref () 获取组件   InstanceType

>利用 InstanceType (实例类型) 来获取组件类型