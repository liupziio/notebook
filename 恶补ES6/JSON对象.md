# JSON



## 注意事项

### 	1.不能有单引号

### 	2.字符串成员需要加上""



## JSON.stringify()

### 	对象转成字符串

```javascript
JSON.stringify({ a: 12, b: 13, c: 13})
=>转成了
{ "a": 12, "b": 13, "c": 13}
```



```javascript
let json = {a:12,b:23,name:"blue"}
	let json = {a:12,b:23,name:"blue"}
        console.log(JSON.stringify(json))
//{"a":12,"b":23,"name":"blue"}
```



## JSON.parse()

## 	字符串转成对象

```javascript
JSON.stringify({ "a": 12, "b": 13, "c": 13})
=>转成了
{ a: 12, b: 13, c: 13}
```



```javascript
let json = {a:12,b:23,name:"blue"}
	let json1 = '{"a":12,"b":23,"name":"blue"}'
    	console.log(JSON.parse(json1))
//{a: 12, b: 23, name: "blue"}
```

