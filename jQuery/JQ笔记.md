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

