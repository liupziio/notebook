

## 1、画出带角的矩形

```css
 .BMapLabel:after {

  content: "";

  position: absolute;

  top: 100%;

  left: 50%;

  transform: translateX(-50%);

  bottom: 0px;

  width: 0px;

  height: 0px;

  border-top: 3px solid transparent;

  border-left: 6px solid #78b725;

  border-bottom: 3px solid transparent;

  transform: rotate(90deg);

 }
```

