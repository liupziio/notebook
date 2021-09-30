# 作用

用来处理异步的回调函数

```js
  <script src="./node_modules/jquery/dist/jquery.js"></script>
    <script>
        let p = new Promise(function(resolve,reject){
            //异步...
            //resolve === 解决
            //reject ===错误驳回
            $.ajax({
                url:'./data/1.txt',//这里文件里边是[1,2,3]
                dataType:'json',
                success(data){
                    resolve(data)
                },
                error(err){
                    reject(err)
                }
                
            })
        })
        p.then(function(data){
            alert('成功');
            console.log(data);//[1,2,3]
        },function(err){
            alert('失败');
            console.log(err);
        })
    </script>
```

