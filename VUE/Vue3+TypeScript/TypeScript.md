# 一、类型使用

## 1.1 定义类型

### 1.1.1 允许类型中可以使用字符串索引

>如果动态访问字符串变量会出现如下问题

```js
export interface IRoom {
  AlmPosition?: string;
  id?: number;
  AlmPointMap?: string;
  Ititle?: string;
  Ivalue?: string;
}
  backRoomName = machineRoom[0][`${machineRoom[0].Ivalue}`];

```



![](F:\learn\note book\VUE\Vue3+TypeScript\TypeScript.assets\image-20220221145326860.png)





```typescript
export interface IRoom {
  AlmPosition?: string;
  id?: number;
  AlmPointMap?: string;
  Ititle?: string;
  Ivalue?: string;
  [key: string]: any;//加上动态key值为string即可
}
 backRoomName = machineRoom[0][`${machineRoom[0].Ivalue}`];
```

