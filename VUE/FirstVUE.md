# VUE

## 官网

https://cn.vuejs.org/



## 视图部分

```js
<body>
    <div id="app">      <!-- 视图编写 -->
        {{message}} , {{name}} , {{age}}
    </div>

  <div id="app_2">      <!-- 视图编写 -->
        <span v-bind:title="message">
            鼠标悬停几秒钟查看此处动态绑定的提示信息！
        </span>
    </div>
</body>
```

## 脚本编写

```js
<script src="../js/vue.js"></script>//引入vue
<script>            //脚本编写
    var app = new Vue({
        el: '#app',//绑定地主
        data: {
            message: 'Hello Vue!',
            name:'我是刘培志',
            age:'20岁'
        }
    })

    var app_2 = new Vue({
        el: '#app_2',//绑定地主
        data: {
            message:'页面加载于 ' + new Date().toString()
        }
       
    })
    app_2.message = "qaq";//在这里又修改,更新了app_2的message的值//响应式
</script>

```

## 执行结果



![](C:\Users\刘培志\Desktop\note book\VUE\img\QQ截图20200509141918.png)