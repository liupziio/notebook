# 一、vue路由

## 1、使用el-menu切换tab时闪烁回到第一个

+ 原因

  + 因为el-menu的初始值index每次加载都会初始一下

+ 解决方案

  + 1、把初始值index设置为空,每次**mounted**中设置每个路由的**menuactive**唯一值

  ```js
   meta: {
        title: '订单管理',
        menuactive: 3,
      },
  ```

  

  + 2、给**.layout-item**设置样式动画变化时延迟

```scss
transition: transform 0.3s;
```



