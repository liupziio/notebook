



+ 使用设计图宽度除以当前html

例子：

+ 设计稿750px 一个块12px 
+ 12px / 100

```js
	var fun = function (doc, win) {
    var docEl = doc.documentElement,
        resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
        recalc = function () {
            var clientWidth = docEl.clientWidth;
            if (!clientWidth) return;

            //这里是假设在640px宽度设计稿的情况下，1rem = 20px；
            //可以根据实际需要修改
            docEl.style.fontSize = 100 * (clientWidth / 750) + 'px';
        };
    if (!doc.addEventListener) return;
    win.addEventListener(resizeEvt, recalc, false);
    doc.addEventListener('DOMContentLoaded', recalc, false);
}
fun(document, window);





 window.onload = function () {
      let setRemsize = function () {
        let width = document.documentElement.clientWidth;
        document.documentElement.style.fontSize = (100 * width) / 750 + "px";
      };
      window.onresize = setRemsize;
      setRemsize();
    };
```



