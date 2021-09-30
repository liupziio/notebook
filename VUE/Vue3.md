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

## customRef（自定义ref）

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
setup() {
    const message = debounceRef("Hello World");
    return {
      message,
    };
  },
```



