# 监听页面的滚动与去除空格

```javascript
$(function(){
	**$(window).scroll(function () { });	// 监听网页的滚动**
**})**
**var res = $.trim(要去除的字符串);//去除空格**
     **$.trim();**
        **作用: 去除字符串两端的空格**
        **参数: 需要去除空格的字符串**
        **返回值: 去除空格之后的字符串**
```

# 选择同级别非当前的

```javascript
**siblings()			/*选择同级别非当前的*/可用于选项卡**
**例：**
**$li.siblings().removeClass("show");//选择到非当前的li并且把非当前li的show属性删除**
**$(this).siblings().removeClass("current");//选择到非当前的这个并且把非当前这个的current属性删除**
```

# 动画

## 左上角到右下角显示隐藏动画



```javascript
$("div").show(1000, function () {   }）	/*div以一秒的左上角到右下角动画来显示*/function可加可不加function中放回调函数，执行完以后干什么**
**$("div").hide(1000, function () {  }）	/*div一秒的右下角到左上角动画来隐藏*/**
**$("div").toggle(1000, function () {  }）	/*div以一秒的动画来切换隐藏或者显示*/**
```



## 上到下切换显示隐藏动画

```
**$("div").slideDown(1000, function () { });	/*div以一秒的上到下动画来显示*/function可加可不加function中放回调函数，执行完以后干什么**
  **$("div").slideUp(1000, function () {});	/*div一秒的下到上动画来隐藏*/**
 **$("div").slideToggle(1000, function () { });/*div以一秒的动画来切换隐藏或者显示*/**
```



## 淡入淡出切换显示隐藏动画

```javascript
 **$("div").fadeIn(1000, function () {});	/*div以一秒的淡入动画来显示*/function可加可不加function中放回调函数，执行完以后干什么**
**$("div").fadeOut(1000, function () {});	/*div一秒的淡出动画来隐藏*/**
**$("div").fadeToggle(1000, function () {});	/*div以一秒的动画来切换隐藏或者显示*/**

```

### 透明度显示隐藏

```javascript
**$("div").fadeTo(1000, 0.2, function () {})/*div以一秒的速度淡入或淡出到0.2透明度的动画来切换隐藏或者显示*/**
```

## 自定义动画animate({})

```javascript
**自定义动画：	$(".two").animate({		//这个函数可以多使用多控制其他的**
                 	   **marginLeft: 500	//第一个参数可以传多个动画同时执行用逗号隔开就可以 marginLeft: 500,width："+=100"不想同时执行就用两个函数**
              		  **}, 5000, "linear", function () {	//第2,3,4个参数**
              		      **// alert("自定义动画执行完毕");**
             		   **});**
	**第一个参数: 接收一个对象, 可以在对象中修改属性	 //执行什么动画/*这个动画可以在当前基础上再加多少*/例如width："+=100"意思是在当前width基础上再加100/*也可以width:"toggle"切换width隐藏出现，也可以放其他的全靠想象*/**
                **第二个参数: 指定动画时长		     	 //执行时间是多少**
                **第三个参数: 指定动画节奏, 默认就是swing	      	//linear是开始慢,中间快,结束慢//swing匀速运动**
                **第四个参数: 动画执行完毕之后的回调函数	    	 //执行结束动画干什么**	
```



## .stop()	停止当前执行的动画



```javascript
$(document).ready(function(){
  $("#start").click(function(){
    $("#box").animate({height:500},"slow");
    $("#box").animate({width:300},"slow");
  });
  $("#stop").click(function(){
//  $("#box").stop();//停止当前动画进入下一个动画
//  $("#box").stop(true);//停止所有动画，并且保持当前的形状
//  $("#box").stop(false,true);//停止当前动画,立即跳到当前动画终点,并且进入下一个动画
  $("#box").stop(true,true);//停止所有动画，并跳转到当前动画的终点，并保持此终点状态。
  });
});
```

## 获取表单提交序列化数据

- .serialize()

```javascript
alert($("form").serialize())
#弹出这个表单的数据
```

## 阻止默认行为

- preventDefault()

```javascript
$("a").click(function(event){
    event.preventDefault();
  });
#阻止a的默认行为
##例如 ：href
```



# 一、选择器



## 1.1 基本选择器

1. id选择器 高级 #id名
2. 类选择器  .类名
3. 元素选择器  P
4. 通配符选择器 * 
5. 群组选择器 

## 1.2 层级选择器

1. 后代选择器 div p
2. 子代选择器 div>P
3. next div+p
4. nextAll div~p

## 1.3 过滤选择器 ：

### 1.3.1 基本过滤选择器

：first、：last 、：not（选择器）、：even、：odd

### 1.3.2 内容过滤选择器

1. ：contains（‘text’）
2. ：empty
3. ：parent
4. ：has（选择器）

### 1.3.3 可见性选择器

1. ：hidden  css  display：none
2. ：visible
3. 属性选择器
4. 子元素选择器
5. nth-child(1) 

# 二、方法



## 2.1 自定义属性data-



+ 可以放置一些后期需要获取的数据
  + data-id=“132”
  + data-cid=“465”

https://blog.csdn.net/mengzuchao/article/details/80503828



```js
<li id="getId" data-id="122" data-vice-id="11">获取id</li>
```



+ 注意点

这里自定义属性赋值，**element** 上是没有变化的，但是获取的是赋值之后的值





+ **getAttribute()方法**

```js
const getId = document.getElementById('getId');
// //getAttribute()取值属性
console.log(getId.getAttribute("data-id"));//122
console.log(getId.getAttribute("data-vice-id"));//11
// //setAttribute()赋值属性
getId.setAttribute("data-id","48");
console.log(getId.getAttribute("data-id"));//48
```



+ **dataset()方法**

```js
//data-前缀属性可以在JS中通过dataset取值，更加方便
console.log(getId.dataset.id);//112
//data-vice-id连接取值使用驼峰命名法取值 
console.log(getId.dataset.viceId);//11
 
//赋值
getId.dataset.id = "113";//113
getId.dataset.viceId--;//10
 
//新增data属性
getId.dataset.id2 = "100";//100
 
//删除，设置成null，或者delete
getId.dataset.id2 = null;//null
delete getId.dataset.id2;//undefind
```



+ **jquery data() 方法**

```js
//获取
var id = $("#getId").data("id"); //122
var viceId = $("#getId").data("vice-id"); //11
//赋值
$("#getId").data("id","100");//100
```



+ **jquery attr()方法**

```js
var id = $("#getId").attr("data-id"); //122
var viceId = $("#getId").attr("data-vice-id"); //11
//赋值
$("#getId").attr("data-id","100");//100
```



# 三、$.ajax()

## 3.1 $.ajax请求格式



```js
$.ajax({
    url:"http://www.microsoft.com",    //请求的url地址
    dataType:"json",   //返回格式为json
    async:true,//请求是否异步，默认为异步，这也是ajax重要特性
    data:{"id":"value"},    //参数值
    type:"POST",   //请求方式
    beforeSend:function(){
        //请求前的处理
    },
    success:function(req){
        //请求成功时处理
    },
    complete:function(){
        //请求完成的处理
    },
    error:function(){
        //请求出错处理
    }
});
```





## 3.2 ajax post 提交formdata参数

```js
　　$.ajax({
　　　　type:'POST',
　　　　url:'/url/path',
　　　　data:formdata,
　　　　/**
　　　　 *必须false才会自动加上正确的Content-Type
　　　　*/
　　　　contentType:false,
　　　　/**
　　　　* 必须false才会避开jQuery对 formdata 的默认处理
　　　　* XMLHttpRequest会对 formdata 进行正确的处理
　　　　*/
        dataType: "json",
　　　　processData:false,
      async:false,
　　    success: function (result) {
                    resolve(result.data)
                },
                error: function () {
                    console.log("上传失败！");
                };

});
```



