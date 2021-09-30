# 父组件必做

1. 把页码和总页码放在 **vuex** 中
2. 在父组件页面中绑定子组件的自定义事件



## 1.数据绑定

+ 需要知道所有数据的条数

```js
//this.all_size 数据条数
this.all_size = res.total;
```

+ 接受数据的数组

```JS
//这里是把请求的每一页都装在这个数组中
//this.all_data 装载数据的数组
this.all_data = this.all_data.concat(res.data);
```

+ 把所有页存在 **vux** 中

```js
//this.$store.state.all_page这个是死的
//this.all_size 数据总条数
//this.size 每页请求的条数
this.$store.state.all_page = Math.ceil(this.all_size / this.size);
```

+ 请求的页数需要绑定在 **vuex** 中

```js
// this.$store.state.page,这个是死的
page: this.$store.state.page,
```



## 2.组件引入与方法调用

+ 引入组件与条件

```js
 // @fatherget这个是死的

<qre-fresh @fatherget="fatherget">
        <div slot="text">
         //这里边装载的是每一条数据，注意不是装载所有数据的容器
        </div>
 </qre-fresh>
```

+ 父组件方法的使用

```js
 //只有传进来的字串是死的,其他都是活的
fatherget(event) {
      if (event == "data") {
        console.log("请求");
        this.getlist(); //请求数据
      } else if (event == "clear") {
        this.all_data = []; //清空数组
        // console.log(this.all_data);
      }
    },
```

