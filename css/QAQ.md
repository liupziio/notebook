# input

## input_type类型

![](C:\Users\刘培志\Desktop\note book\css\img\input_type.png)



## 边框

#### 去除未选中状态边框

```css
  border: 0;
```

#### 去除选中状态边框

```csss
outline: none;
```



# a标签

## 四种状态

```css
a:link - 普通的、未被访问的链接
a:visited - 用户已访问的链接
a:hover - 鼠标指针位于链接的上方
a:active - 链接被点击的时刻
```

## 去除下划线

```css
text-decoration: none;
```

# 表单

## 文字在中间两边有线

```javascript
#这样可以让字居中一圈线，如果想要只有两边有线那就删除
// border-bottom: 0;
    border-left: 0;
    border-right: 0;

<fieldset>
	<legend align="center">其他方式登录</legend>
</fieldset>

```

