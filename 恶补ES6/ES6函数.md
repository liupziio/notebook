# 箭头函数

```javascript
 let arr = [12,45,3,84,76]
	#原生js
        // arr.sort(function(n1,n2){
        //     return n1-n2
        // })
    #箭头函数
        arr.sort((n1,n2)=>{  return n1-n2})
        
        alert(arr)
//3,12,45,76,84
```

## 箭头函数简写

### 条件

#### 1.如果有且只有一个参数（）也可以不写

```javascript
      // function add(n){
        //     return n+5
        // }

        function show(n,fn){
            alert(fn(n))
        }
        show(12,n=>n+5)//这里的箭头函数等于上边的注释函数
        	//17
```



#### 2.如果有且只有一个语句并且返回的是return的{}也可以不写

```javascript
arr.sort((n1,n2)=>n1-n2)
```



#### 3.修正this（固定）

+ 明确指当前所在的环境



# 参数

## 收集剩余参数

```javascript
 function show(a,b,...c){//a,b各自是一个参数,剩余参数c来搜集
            console.log(a,b,c)
        }
        show(1,2,3,4,5,6,7)
	//1 2 [3, 4, 5, 6, 7]
```

## 展开参数

```javascript
let arr1 = [1,2,3] 
function show(a,b,c){
             alert(a+b+c)
         }
        show(...arr1)//把数组展开到show函数里
	//6
```

## 数组拼接

```javascript
 let arr1 = [1,2,3]
 let arr2 = [4,5,6]
 let arr = [...arr1,...arr2]//拼接数组
 alert(arr)
	//1,2,3,4,5,6
```

## json拼接

```javascript
 let json = {a:1,b:2,c:3}
        let json1 = {
            ...json,
            d:4
        }//把json数据拼接
        console.log(json1)
	//{a:1,b:2,c:3,d:4}
```

# arr数组扩展

## map 映射

+ map 映射 一个对一个
+ [ 60,24,70]=>[ '及格', '不及格', '及格' ]

### 应用

#### 原生函数+三目运算符

```javascript
  let arr = [60,24,70]

  let arr1 = arr.map(function(item){//传一个参数设值
             // if(item>=60){
             //     return '及格'
             // }else{
             //     return '不及格'
             // }
             return item>=60?'及格':'不及格';
             #返回条件 item>=60'返回'及格'否则返回'不及格
       })
  console.log(arr1)
	//["及格", "不及格", "及格"]
```

#### 箭头函数+三目运算符

```javascript
let arr = [ 60,24,70]
 let arr1 = arr.map(item=> item>=60?'及格':'不及格')
            console.log(arr1)
	//["及格", "不及格", "及格"]
```



## reduce 汇总

+ reduce 汇总 一堆出来一个

### 用于汇总比如，算个总数，算个平均

```javascript
let arr = [1, 3, 5, 7,6]
//1+3
//tmp+item
//4+5
//tmp+item
let result = arr.reduce(function(tmp,item,index){
      //tmp 上次结果，item当前数，index第几次计算次数1开始
           return tmp+item
        })
        alert(result/arr.length)//求平均
	//4.4
```





## filter 过滤

### filter 过滤器 保留为true的

```javascript
  let arr = [68,53,98,65,83]

 let arr2 = arr.filter(item=>item%2==1?true:false)
 //item是行参数(用于比较，相当于等于这个对象)
        console.log(arr2)
//[53, 65, 83]
```



```javascript
var aa = [
    { title: '苹果', price: 10 },
    { title: '西瓜', price: 20 },
           ]
var result = aa.filter(json => json.price >= 20)
//json是行参(用于比较，相当于等于这个对象)
console.log(result)
//title: "西瓜",price: 20
```





## forEach 遍历

### 用于循环迭代

```javascript
let arr = [1,2,3,4,5,6]
             arr.forEach((item,index)=>console.log(`${item}:是第${index}个`))
//item代表当前这个数

1:是第0个
2:是第1个
3:是第2个
4:是第3个
5:是第4个
6:是第5个
```



