# 一、设计模型

## 1.1 MVVM 设计模型

### 什么是MVC

> MVVM是Model-View-Controller的简写

+ Model：数据模型
  + 用来存储数据
+ View视图界面
  + 用来展示UI界面和响应用户交互
+ Controller
  + 控制器(大管家角色)，监听模型数据的改变和控制视图行为、处理用户交互

### 什么是mvvm

> MVVM是Model-View-ViewModel的简写

mvvm 实现了数据驱动

+ Model 
  + 后台获取的数据
+ view 
  + 用户看到的页面
+ ViewModel 
  + 连接view和model的桥梁。