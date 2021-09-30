# 一、表单

## 注意点

1、在设置表单是最外层都会有一个容器

+ ```js
  <div class="container">
  ```



2、form里边要定义一个角色

+ ```js
  <form action="" role="form">
  ```



3、最好每一个表单元素占一个div





## 1.0、垂直表单实例



```js
<!--垂直表单-->
			<form action="" role="form">
				<!--用户名-->
				<div class="form-group">
					<!--每一个表单元素占一个div,class是form-group-->
					<label for="name">用户名:</label>
					<!--form-control找到表单控制的对象-->
					<input type="text" class="form-control" id="name" />
				</div>
				
				<!--密码-->
				<div class="form-group">
					<label for="password">密码:</label>
					<!--form-control找到表单控制的对象-->
					<input type="password" class="form-control" id="password" />
				</div>
				
				<!--提交-->
				<div class="form-group">
					<!--默认按钮default-->
					<button type="submit" class="btn btn-default">提交</button>
				</div>
				
				<!--重置-->
				<div class="form-group">
					<!--默认按钮default-->
					<button type="submit" class="btn btn-default">重置</button>
				</div>
				
				
			</form>
```



## 2.0、内联表单实例



```js
<!--内联表单 --> 	
			<form action="" role="form" class="form-inline">
				<!--内联表单需要加上class类: form-inline-->
				<!--用户名-->
				<div class="form-group">
					<!--每一个表单元素占一个div,class是form-group-->
					<label for="name">用户名:</label>
					<!--form-control找到表单控制的对象-->
					<input type="text" class="form-control " id="name" />
				</div>
				
				<!--密码-->
				<div class="form-group">
					<label for="password">密码:</label>
					<!--form-control找到表单控制的对象-->
					<input type="password" class="form-control " id="password" />
				</div>
				
				<!--提交-->
				<div class="form-group">
					<!--默认按钮default-->
					<button type="submit" class="btn btn-default">提交</button>
				</div>
				
				<!--重置-->
				<div class="form-group">
					<!--默认按钮default-->
					<button type="submit" class="btn btn-default">重置</button>
				</div>
				
				
			</form>
```



## 3.0、水平表单和垂直表单结合



```js
<form action="" role="form" class="form-horizontal">
				<!--内联表单需要加上class类: form-horizontal-->
				
				<!--用户名-->
				<div class="form-group">
					
					<!--每一个表单元素占一个div,class是form-group-->
					<label for="name" class="col-lg-2 control-label">用户名:</label>
					<!--form-control代表这个框是form控制的-->
					<div class="col-lg-10">
						<input type="text" class="form-control" id="name" placeholder="请输入用户名" />
					</div>
				</div>
				
				<!--密码-->
				<div class="form-group">
					<label class="col-lg-2 control-label" for="password">密码:</label>
					<!--form-control代表这个框是form控制的-->
					<div class="col-lg-10">
						<input type="password" class="form-control" id="password" placeholder="密码" />
					</div>
				</div>
				
				<!--提交-->
				<div class="form-group">
					<!--默认按钮default-->
					<div class="col-lg-1 col-lg-offset-2">
						<button type="submit" class="btn btn-default">提交</button>
					</div>
				
					<!--重置-->
					<!--默认按钮default-->
					<div class="col-lg-1">
						<button type="submit" class="btn btn-default ">重置</button>
					</div>
				</div>
				
				
			</form>			
```



### 文本说明

1. 利用水平表单实现了水平让**文字**和**输入框**并排
2. 利用右偏移实现了让**登录**与**重置**按钮移动到顺眼地方