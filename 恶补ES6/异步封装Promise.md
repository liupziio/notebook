# Ajax自带的promise

## 封装一个请求返回一个数据

### 写法

```js
  $.ajax({
            url:'./data/1.txt',
            dataType:'json'
        }).then(data=>{//第一个回调函数是数据
            alert('成功')
            console.log(data)
        },err=>{//第二个回调函数是错误
            alert('失败') 
            console.log(err)
        })
```



# Promise.all([ ajax请求 ])



## 放入多个请求并且返回各自的数据



### ES6写法

```js
 Promise.all([             //Promise.all([ ajax请求 ])可以放入多个请求最后一个.then利用多个参数返回结果
            $.ajax({url:'./data/1.txt',dataType:'json'}),
            $.ajax({url:'./data/2.txt',dataType:'json'}),
            $.ajax({url:'./data/3.txt',dataType:'json'})
        ]).then(([data1,data2,data3])=>{     //ES6的箭头函数这里需要加【】
             alert('成功')
             console.log(data1,data2,data3)
         },res=>{
             alert('失败')
             console.log(res)
         })
```



### 原生JS写法

```js
Promise.all([           //Promise.all([ ajax请求 ])可以放入多个请求最后一个.then利用多个参数返回结果
            $.ajax({url:'./data/1.txt',dataType:'json'}),
            $.ajax({url:'./data/2.txt',dataType:'json'}),
            $.ajax({url:'./data/3.txt',dataType:'json'})
        ]).then((function (data1,data2,data3) {     //原生js这里不需要加【】
           
             alert('成功')
             console.log(data1,data2,data3)
        
        }),function (res) {
             alert('失败')
             console.log(res)
         })
```

# async/await挑选出个别请求

## 作用

+ 如果碰到想用使用的请求可以区分出来！！！

## 写法

```js
<script src="./node_modules/jquery/dist/jquery.js"></script>

    <script>
        async function show() {
            let a = 12;
            let b = 23;

            try {//try监听try{}中的错误数据
                //当前data就等于这个异步Ajax中的数据
                let data = await $.ajax({ url: './data/1.txt', dataType: 'json' })

                alert(a + b + data[0])
            } catch (e) {//如果出错执行
                alert('读取错误')
                // console.log(e)
            }



        }
        show();
    </script>
```

