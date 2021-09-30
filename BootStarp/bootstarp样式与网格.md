| **向左浮动****pull** | xs- pull- * | sm- pull- * | md- pull- * | lg- pull- * |
| -------------------- | ----------- | ----------- | ----------- | ----------- |
| **向右浮动****push** | xs- push- * | sm- push- * | md- push- * | lg- push- * |

# 样式

## 图片样式

- .img-rounded	让图片获得圆角

```javascript
#添加 border-radius:6px 来获得图片圆角。
 <img src="images/1.png" alt="图片" class="img-rounded">
```



- .img-circle	让整个图片变成圆形

```javascript
#添加 border-radius:50% 来让整个图片变成圆形。
<img src="images/1.png" alt="图片" class="img-circle">
```



- .img-thumbnail	让图片添加一些padding和一个灰色的边框。

```javascript
<img src="images/1.png" alt="图片" class="img-thumbnail">
```



- .img-responsive	可以支持图片响应式布局

```javascript
#其实质是为图片设置了属性“max-width: 100%;height: auto; display: block;”，从而让图片在其父元素中更好地缩放。
<img src="images/1.png" alt="图片" class="img-responsive">
```



- .center-block	可以让图片（在div）水平居中显示

```html
<img src="images/1.png" alt="图片" class="center-block">
```



## 文本样式

+ .lead	会让段落突出显示

```html
<p class="lead">段落2</p>
```



+ <small></small>或者加入.small	会使用副标签

```html
<h1>Bootstrap 标题1 <small>Bootstrap 小标题</small></h1>

<h1>Bootstrap 标题1 <span class="small">Bootstrap 小标题</span></h1>
```



+ 标题	超大屏幕

```html
<div class="container">
             <div class="jumbotron">
	            <h1>欢迎登陆页面！</h1>
	            <p>这是一个超大屏幕（Jumbotron）的实例。</p>
	            <p><a class="btn btn-primary btn-lg" role="button">学习更多</a></p>
       		</div>
        </div>
```


+ 缩略语 ,只显示boot移动上去显示全部

```html
 <abbr title="Bootstarp">Boot</abbr>
```



+ <mark></mark>或者 .mark	标记文本

```html
<p>内联<mark>我是被标记文本</mark></p>
<p>内联<span class="mark">我是被标记文本</span></p>
```



+ <del>和<s>	添加中间删除线

```html
<del>内联元素</del>			<s>内联元素</s>  
```



+ <ins>和<u>	添加下划线

```html
<ins>内联元素</ins>			<u>内联元素</u>  
```



+ <strong>	字体加粗 	<em>	字体倾斜

```html
<strong>内联元素</strong>	<em>内联元素</em>   
```



+ .text-left	-center	-right	文本居左、中、右

```html
<p class="text-left">Bootstrap 对齐</p>        
<p class="text-center">Bootstrap 对齐</p>      
<p class="text-right">Bootstrap 对齐</p>  
```



+ 页面元素居中

```javascript
<div class="center-block">居中</div>
```



+ .text-lowercase -uppercase -capitalize	字母转为大小写首字母大写

```html
<p class="text-lowercase">Bootstrap 转大写</p>       
<p class="text-uppercase">Bootstrap 转小写</p>       
<p class="text-capitalize">app 首字母大写</p>  
```



+ 《blockquote》文本居左.blockquote-reverse.pull-right居右

```html
<blockquote>居左引用文本</blockquote>
<blockquote  class="blockquote-reverse ">居右文本1</blockquote>
<blockquote  class="pull-right ">居右文本2</blockquote>
```



+ . list-unstyled类：移除默认样式，即去掉列表前的小黑点。
+ . list-inline类：设为内联，使得列表从垂直排列变为水平排列
+ 使用. dl-horizontal类可使定义列表水平排列

```html
<ul class="list-unstyled">list-inline/dl-horizontal
	<li>列表样式1</li>
	<li>列表样式2</li>
	<li>列表样式3</li>
</ul>
```

## 辅助类

### 按钮 辅助类

+ 象征的出现一个"X"图标

```html
<button type="button" class="close">&times;</button>
```

![](C:\Users\刘培志\Desktop\note book\BootStarp\img\图片1.png)

+ 象征性的出现一个三角符号可用于下拉菜单

![](C:\Users\刘培志\Desktop\note book\BootStarp\img\图片2.png)



### 浮动隐现 辅助类

+ 快速浮动类.pull-left和.pull-right

```html
<span class="pull-left">我是1</span>
<span class="pull-right">我是2</span>
```

+ div居中，div清除浮动，显示与隐藏

```html
<div class="center-block">居中</div>
<div class="clearfix">清除浮动</div>
<div class="show">显示</div>
<div class="hidden">隐藏</div>
```



### 表单 辅助类

+ 背景颜色

| **类**                  | **描述**             |
| ----------------------- | -------------------- |
| **. text/.bg- muted**   | 文本/背景   柔和——灰 |
| **. text/.bg- primary** | 文本/背景   主要——蓝 |
| **. text/.bg- success** | 文本/背景   成功——绿 |
| **. text/.bg- info**    | 文本/背景   信息——蓝 |
| **. text/.bg- warning** | 文本/背景   警告——黄 |
| **. text/.bg- danger**  | 文本/背景   危险——红 |



## 表格样式

+ https://www.runoob.com/bootstrap/bootstrap-tables.html

+ | **.active**            | 对某一特定的行或单元格应用悬停颜色                           |
  | ---------------------- | :----------------------------------------------------------- |
  | **.success**           | 表示一个成功的或积极的动作                                   |
  | **.warning**           | 表示一个需要注意的警告                                       |
  | **.danger**            | 表示一个危险的或潜在的负面动作                               |
  | .table                 | 添加简单基础表格                                             |
  | .table-bordered        | 添加边框                                                     |
  | .table-hover           | 悬停效果                                                     |
  | .table-striped         | 隔行变色                                                     |
  | .sr-only               | 隐藏当前行                                                   |
  | .table-responsive      | 实现响应式表格。表格父元素设置响应式，当屏幕小于768px时，表格就会自适应，出现边框，多的隐藏可以滚动<body class="table-responsive"> |
  | .table-condensed class | 行内边距（padding）被切为两半，可让表看起来更紧凑。          |

```javascript
<table class="table table-striped table-bordered table-hover table-responsive table-condensed">
			<tr><th>姓名</th><th>性别</th><th>年龄</th></tr>
			<tr class="active"><td>张三</td><td>男</td><td>1</td></tr>
			<tr class="success"><td>李四</td><td>女</td><td>2</td></tr>
			<tr class="sr-only"><td>王明</td><td>男</td><td>3</td></tr>
			<tr class="warning"><td>麻五</td><td>男</td><td>4</td></tr>
			<tr class="danger"><td>六子</td><td>男</td><td>5</td></tr>
			
		</table>
```

![](C:\Users\刘培志\Desktop\note book\BootStarp\img\图片4.png)

+ dl 表单

```html
<dl class="dl-horizontal"> <!--标题头-->
	        	<dt>Bootstrap</dt>
				 <dd>Bootstrap 页面排版的样式</dd>
				 <dt>Bootstrap</dt>
				 <dd>Bootstrap 页面排版的样式</dd>
				 <dt>Bootstrap</dt>
				 <dd>Bootstrap 页面排版的样式</dd>
	        </dl>
```

![](C:\Users\刘培志\Desktop\note book\BootStarp\img\QQ截图20200429094804.png)

## 徽章

https://www.runoob.com/bootstrap4/bootstrap4-badges.html

| .nav nav-pills   | 让他出现特效“胶囊” |
| ---------------- | ------------------ |
| .btn btn-success | 积极的颜色         |
| .badge           | 添加徽章:提示      |

```html
<ul class="nav nav-pills">  
       <li class="active">
               <a href="#">首页 <span class="badge">2</span></a>
       </li>
       <li><a href="#">资讯</a></li>
       <button class="btn btn-success"><span class="badge">3</span></button>
	</ul>
```
## 字体图标

https://www.runoob.com/bootstrap/bootstrap-glyphicons.html



https://v3.bootcss.com/components/

+ 各种形状+-=%*

![](C:\Users\刘培志\Desktop\note book\BootStarp\img\QQ截图20200427115436.png)







# 响应式布局



## 响应式网格布局

|                        | 超小设备手机（<768px）         | 小型设备平板电脑（≥768px）     | 中型设备台式电脑（≥992px）     | 大型设备台式电脑（≥1200px）    |
| :--------------------- | :----------------------------- | :----------------------------- | :----------------------------- | ------------------------------ |
| 网格行为               | 一直是水平的                   | 以折叠开始，断点以上是水平的   | 以折叠开始，断点以上是水平的   | 以折叠开始，断点以上是水平的   |
| 最大容器宽度           | None (auto)                    | 750px                          | 970px                          | 1170px                         |
| **Class 前缀**         | **.col-xs-***                  | **.col-sm-***                  | **.col-md-***                  | **.col-lg-***                  |
| **设置列偏移，向右偏** | **xs- offset- ***              | **sm- offset- ***              | **md- offset- ***              | **lg- offset- ***              |
| **向左浮动pul**l       | **xs- pull- ***                | **sm- pull- ***                | **md- pull- ***                | **lg- pull- ***                |
| **向右浮动push**       | **xs- push- ***                | **sm- push- ***                | **md- push- ***                | **lg- push- ***                |
| 列数量和               | 12                             | 12                             | 12                             | 12                             |
| 最大列宽               | Auto                           | 60px                           | 78px                           | 95px                           |
| 间隙宽度               | 30px （一个列的每边分别 15px） | 30px （一个列的每边分别 15px） | 30px （一个列的每边分别 15px） | 30px （一个列的每边分别 15px） |
| 可嵌套                 | Yes                            | Yes                            | Yes                            | Yes                            |
| 偏移量                 | Yes                            | Yes                            | Yes                            | Yes                            |
| 列排序                 | Yes                            | Yes                            | Yes                            | Yes                            |

### 注意点

+ 列偏移和向右浮动的区别
  + 区别在于列偏移会带着列中的其他 “行” 动
  + 而pull右浮动只会自己浮动
+ div class="containner"
  + 最外边

+ div class="row"
  + 行，在这里添加列宽与浮动偏移

