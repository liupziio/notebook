# 一、方法



## 1.自定义属性data-



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



## 二、$.ajax()



### 1、ajax post 提交formdata参数

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



