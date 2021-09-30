 transform: scale(1.3);

 transform-origin: 0 10% 6;

# transform(2D，3D动画)

## 文本说明

1. 可以灵活运用不要死脑筋

```js
transform:translate(10px, 20px) rotate(30deg) scale(1.5, 2); //这样也是可以的
```



## 1、transform-origin设置基线在哪

```css
 /* transform-origin: x轴 y轴 z轴; */
    transform-origin: 70% -20%;
x,y轴可填				z轴
left					length
center
right
length
%
```





## 2、transform旋转rotate

```css
 /* 正值向顺时针方向，负值相反 deg(度) */

	transform:rotate(30deg)
```



## 3、transform移动translate

```css
  /* 移动translate我们分为三种情况：
            translate(x,y)水平方向和垂直方向同时移动（也就是X轴和Y轴同时移动）；
            translateX(x)仅水平方向移动（X轴移动）；
            translateY(Y)仅垂直方向移动（Y轴移动），
             */
             transform:translate(200px,200px)
```



## 4、transform缩放scale

+ 结合transform-origin设置基线更好

```css
/* 缩放scale和移动translate是极其相似，他也具有三种情况：
             scale(x,y)使元素水平方向和垂直方向同时缩放（也就是X轴和Y轴同时缩 放）；
             scaleX(x)元素仅水平方向缩放（X轴缩放）；scaleY(y)元素仅垂直方向缩放（Y轴缩放），
             但它们具有相同的缩放中心点和基数，其中 心点就是元素的中心位置，缩放基数为1，如果其值大于1元素就放大，反之其值小于1，元素缩小。 */
             transform:scaleY(2)

```



## 5、transform扭曲skew

```css
 /* 扭曲skew和translate、scale一样同样具有三种情况：
            skew(x,y)使元素在水平和垂直方向同时扭曲（X轴和Y轴同时按一定的角度值 进行扭曲变形）；
            skewX(x)仅使元素在水平方向扭曲变形（X轴扭曲变形）；
            skewY(y)仅使元素在垂直方向扭曲变形（Y轴扭曲变形） */
             transform:skew(30deg,10deg)
```

