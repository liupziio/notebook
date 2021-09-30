**overflow: hidden;/*以当前px裁剪,内容会被修剪，并且其余内容是不可见的*/**
**position: fixed 	//固定定位定位滚动时固定不动**
**transition:  height .7s ease .2s,box-shadow .1s ease .3s;	//过渡动画**
**/*变化height 以0.7s完成; 执行这个动画准备时间 0.2s,盒子的阴影 以0.1s执行结束 执行阴影准备时间0.3s*/**

**box-shadow: h-shadow v-shadow blur spread color inset；**

**h-shadow	必需。水平阴影的位置。允许负值。	测试**
**v-shadow	必需。垂直阴影的位置。允许负值。	测试**
**blur	可选。模糊距离。	测试**
**spread	可选。阴影的尺寸。	测试**
**color	可选。阴影的颜色。请参阅 CSS 颜色值。	测试**
**inset	可选。将外部阴影 (outset) 改为内部阴影。**

**cursor: pointer;	/*鼠标移上去添加小手指*/**
 **display: inline-block; /*设置行内元素*/**
 **transform: rotate(90deg);/*旋转90度*/ transform:** 

**表单必填项:**不然会弹出提示

**required minlength="2" maxlength="10"**

**//最大10个最小2个，必须这样不然会弹提示**

### 背景图大小

```javascript
#背景图填满整个容器
background-size:cover;
background-size:auto;/* 默认值，不改变背景图片的高度和宽度 */
background-size:100px 50px;/* 第一个值为宽，第二个值为高，当设置一个值时，将其作为图片宽度来等比缩放 */
background-size:10%;/* 0％~100％之间的任何值，将背景图片宽高按百分比显示，当设置一个值的时候同也将其作为图片宽度来等比缩放 */
background-size:cover;/* 将背景图片等比缩放填满整个容器 */
background-size:contain;/* 将背景图片等比缩放至某一边紧贴容器边缘 */
```

### 表单占位符

```javascript
  <input type="email" placeholder="请输入账号">
#把placeholder写入文本框内：placeholder=“请输入账号”，在页面点击文本框时，文本框里显示“请输入账号“，当输入文字时，placeholder里的内容（请输入账号）隐藏（消失）
```







# 网页

## 1.滚动

### 滚动到一定位置定在那，

+ 回到一定位置，回原地

```
 .tab-control {/* 处理选项卡的粘贴属性 */

  position: sticky;

  top:44px;

 }
```

### 隐藏滚动条

```css
/* 隐藏滚动条 */
#container::-webkit-scrollbar {
    display: none;
}
```



### 自定义滚动条

```js
    <style>
      .test {
        width: 50px;
        height: 200px;
        overflow: auto;
        float: left;
        margin: 5px;
        border: none;
      }
      .scrollbar {
        width: 30px;
        height: 300px;
        margin: 0 auto;
      }
      .test-1::-webkit-scrollbar {
        /*滚动条整体样式*/
        width: 10px; /*高宽分别对应横竖滚动条的尺寸*/
        height: 1px;
      }
      .test-1::-webkit-scrollbar-thumb {
        /*滚动条里面小方块*/
        border-radius: 10px;
        box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
        background: #535353;
      }
      .test-1::-webkit-scrollbar-track {
        /*滚动条里面轨道*/
        box-shadow: inset 0 0 5px rgba(0, 0, 0, 0.2);
        border-radius: 10px;
        background: #ededed;
      }
    </style>


  <div class="test test-1">
      <div class="scrollbar"></div>
    </div>
```





# 文本



## 文本超出部门显示省略号



```css
/* 文本超出宽度不换行 */
    white-space: nowrap;
    /* 超出部门隐藏 */
    overflow: hidden;
    /* 文本超出部门显示省略号 */
    text-overflow: ellipsis;
```



## 文本超出多少行显示省略号



```css
  display: -webkit-box;
  overflow: hidden;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  align-self: start;
```



## 文本超出宽度换行显示

```css
    overflow: hidden;
    white-space: normal;
    word-break: break-all;
设置div的宽度（width），当超过宽度时，则隐藏字符（overflow:hidden）,同时设置white-space属性为normal，word-break属性为break-all，实现将字符强制性换行。
```



## 文字间隔

```css
letter-spacing: 5px;
```





# 去除css自带样式



## input去除自带样式

```css
    /* 背景色清空 */
    background: none;
    /* 去除border */
     border: none;
    /* 去掉选中的默认样式 */
    outline: none;
```





## select去除自带样式

```css
/* 背景色清空 */
background: none;
/* 去除border */
      border: none;
/* 去除下箭头 */
       appearance:none;
/* 去掉选中的默认样式 */
outline: none;

```



## button去除默认样式

```css
/* 去除border */
border: 0;
 /* 背景色透明 */
background-color: transparent;
 /* 去掉选中的默认样式 */
outline: none;
```



# 用户设置



## 不让用户复制文字

```css
user-select:none;
```



