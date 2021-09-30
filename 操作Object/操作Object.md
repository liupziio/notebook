# 一、遍历每一个键值

## 1、清空对象中的每一个键值

```js
#obj === 对象
    Object.keys(obj).forEach(key=>obj[key]='')
```

## 2、判断对象中的键是否都为空

```js
   let arr = Object.values(this.query).filter(function(item) {
                    if (item !== '') {
                        return true
                    }
                })
                console.log(arr);
                if (arr.length === 0) {
                    this.$alert('至少输入一个查询条件', '查询提示', {
                        confirmButtonText: '确定',
                    });
                    return
                }
                console.log(this.query);
```



## 3、遍历对象Object

```js
  for (const key in this.form) {
        if(key === "ma_people_num"){
        this.form[key] = 1
        continue
        }
        this.form[key] = ""
      }
```

