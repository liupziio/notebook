# 一、node文档



## 1.1 监听事件

### 1.1.1 Node.js EventEmitter

> Node.js 所有的异步 I/O 操作在完成时都会发送一个事件到事件队列。
>
> Node.js 里面的许多对象都会分发事件：一个 net.Server 对象会在每次有新连接时触发一个事件， 一个 fs.readStream 对象会在文件被打开的时候触发一个事件。 所有这些产生事件的对象都是 events.EventEmitter 的实例。

#### 方法

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **addListener(event, listener)** 为指定事件添加一个监听器到监听器数组的尾部。 |
| 2    | **on(event, listener)** 为指定事件注册一个监听器，接受一个字符串 event 和一个回调函数。`server.on('connection', function (stream) {  console.log('someone connected!'); });` |
| 3    | **once(event, listener)** 为指定事件注册一个单次监听器，即 监听器最多只会触发一次，触发后立刻解除该监听器。`server.once('connection', function (stream) {  console.log('Ah, we have our first user!'); });` |
| 4    | **removeListener(event, listener)** 移除指定事件的某个监听器，监听器必须是该事件已经注册过的监听器。它接受两个参数，第一个是事件名称，第二个是回调函数名称。`var callback = function(stream) {  console.log('someone connected!'); }; server.on('connection', callback); // ... server.removeListener('connection', callback);` |
| 5    | **removeAllListeners([event])** 移除所有事件的所有监听器， 如果指定事件，则移除指定事件的所有监听器。 |
| 6    | **setMaxListeners(n)** 默认情况下， EventEmitters 如果你添加的监听器超过 10 个就会输出警告信息。 setMaxListeners 函数用于改变监听器的默认限制的数量。 |
| 7    | **listeners(event)** 返回指定事件的监听器数组。              |
| 8    | **emit(event, [arg1], [arg2], [...])** 按监听器的顺序执行执行每个监听器，如果事件有注册监听返回 true，否则返回 false。 |

#### 类方法

| 序号 | 方法 & 描述                                                  |
| :--- | :----------------------------------------------------------- |
| 1    | **listenerCount(emitter, event)** 返回指定事件的监听器数量。 |

```
events.EventEmitter.listenerCount(emitter, eventName) //已废弃，不推荐
events.emitter.listenerCount(eventName) //推荐
```

#### 实例

```js
var events = require("events");
var eventEmitter = new events.EventEmitter();

// 监听器 #1
var listener1 = function listener1() {
  console.log("监听器 listener1 执行。");
};

// 监听器 #2
var listener2 = function listener2() {
  console.log("监听器 listener2 执行。");
};

// 绑定 connection 事件，处理函数为 listener1
eventEmitter.addListener("connection", listener1);

// 绑定 connection 事件，处理函数为 listener2
eventEmitter.on("connection", listener2);

var eventListeners = eventEmitter.listenerCount("connection");
console.log(eventListeners + " 个监听器监听连接事件。");

// 处理 connection 事件
eventEmitter.emit("connection");

// 移除监绑定的 listener1 函数
eventEmitter.removeListener("connection", listener1);
console.log("listener1 不再受监听。");

// 触发连接事件
eventEmitter.emit("connection");

eventListeners = eventEmitter.listenerCount("connection");
console.log(eventListeners + " 个监听器监听连接事件。");

console.log("程序执行完毕。");

```

```
$ node main.js
2 个监听器监听连接事件。
监听器 listener1 执行。
监听器 listener2 执行。
listener1 不再受监听。
监听器 listener2 执行。
1 个监听器监听连接事件。
程序执行完毕。
```

#### 继承 EventEmitter

**大多数时候我们不会直接使用 EventEmitter**

> 大多数时候我们不会直接使用 EventEmitter，而是在对象中继承它。包括 fs、net、 http 在内的，只要是支持事件响应的核心模块都是 EventEmitter 的子类。
>
> 为什么要这样做呢？原因有两点：
>
> 首先，具有某个实体功能的对象实现事件符合语义， 事件的监听和发生应该是一个对象的方法。
>
> 其次 JavaScript 的对象机制是基于原型的，支持 部分多重继承，继承 EventEmitter 不会打乱对象原有的继承关系。



## 1.2 Node.js Buffer(缓冲区)

>**JavaScript 语言自身只有字符串数据类型，没有二进制数据类型。**
>
>但在处理像**TCP流**或**文件流**时，必须使用到二进制数据。因此在 Node.js中，定义了一个 Buffer 类，该类用来创建一个专门存放二进制数据的缓存区。
>
>在 Node.js 中，Buffer 类是随 Node 内核一起发布的核心库。Buffer 库为 Node.js 带来了一种存储原始数据的方法，可以让 Node.js 处理二进制数据，**每当需要在 Node.js 中处理I/O操作中移动的数据时，就有可能使用 Buffer 库。原始数据存储在 Buffer 类的实例中。一个 Buffer 类似于一个整数数组，但它对应于 V8 堆内存之外的一块原始内存。**



## 1.3 Node.js Stream(流)

### 1.3.1 说明

> Stream 是一个抽象接口，Node 中有很多对象实现了这个接口。例如，对http 服务器发起请求的request 对象就是一个 Stream，还有stdout（标准输出）。



##### 所属作者：

 [菜鸟教程 NodeJs](https://www.runoob.com/nodejs/nodejs-stream.html)



### 1.3.2 操作流

#### 流类型

+ Node.js，Stream 有四种流类型：

| 序号 | 类型          | 描述                         |
| :--- | ------------- | ---------------------------- |
| 1    | **Readable**  | 可读操作                     |
| 2    | **Writable**  | 可写操作                     |
| 3    | **Duplex**    | 可读可写操作                 |
| 4    | **Transform** | 操作被写入数据，然后读出结果 |



+ 所有的 Stream 对象都是 EventEmitter 的实例。常用的事件有：

| 序号 | 类型       | 描述                               |
| :--- | ---------- | ---------------------------------- |
| 1    | **data**   | 当有数据可读时触发。               |
| 2    | **end**    | 没有更多的数据可读时触发。         |
| 3    | **error**  | 在接收和写入过程中发生错误时触发。 |
| 4    | **finish** | 所有数据已被写入到底层系统时触发。 |



#### 从流中读取数据

创建 input.txt 文件，内容如下：

```
菜鸟教程官网地址：www.runoob.com
```

创建 main.js 文件, 代码如下：

```js
var fs = require("fs");
var data = '';

// 创建可读流
var readerStream = fs.createReadStream('input.txt');

// 设置编码为 utf8。
readerStream.setEncoding('UTF8');

// 处理流事件 --> data, end, and error
readerStream.on('data', function(chunk) {
   data += chunk;
});

readerStream.on('end',function(){
   console.log(data);
});

readerStream.on('error', function(err){
   console.log(err.stack);
});

console.log("程序执行完毕");
```

以上代码执行结果如下：

```
程序执行完毕
菜鸟教程官网地址：www.runoob.com
```





#### 写入流

创建 main.js 文件, 代码如下：

```js
var fs = require("fs");
var data = '菜鸟教程官网地址：www.runoob.com';

// 创建一个可以写入的流，写入到文件 output.txt 中
var writerStream = fs.createWriteStream('output.txt');

// 使用 utf8 编码写入数据
writerStream.write(data,'UTF8');

// 标记文件末尾
writerStream.end();

// 处理流事件 --> finish、error
writerStream.on('finish', function() {
    console.log("写入完成。");
});

writerStream.on('error', function(err){
   console.log(err.stack);
});

console.log("程序执行完毕");
```

以上程序会将 data 变量的数据写入到 output.txt 文件中。代码执行结果如下：

```
$ node main.js 
程序执行完毕
写入完成。
```

查看 output.txt 文件的内容：

```
$ cat output.txt 
菜鸟教程官网地址：www.runoob.com
```





#### 将a文件的数据写入b文件中



设置 input.txt 文件内容如下：

```
菜鸟教程官网地址：www.runoob.com
管道流操作实例
```

创建 main.js 文件, 代码如下：

```js
var fs = require("fs");

// 创建一个可读流
var readerStream = fs.createReadStream('input.txt');

// 创建一个可写流
var writerStream = fs.createWriteStream('output.txt');

// 管道读写操作
// 读取 input.txt 文件内容，并将内容写入到 output.txt 文件中
readerStream.pipe(writerStream);

console.log("程序执行完毕");
```

代码执行结果如下：

```
$ node main.js 
程序执行完毕
```

查看 output.txt 文件的内容：

```
$ cat output.txt 
菜鸟教程官网地址：www.runoob.com
管道流操作实例
```

#### 链式流

##### 链式流(压缩文件为 gz)

创建 compress.js 文件, 代码如下：

```js
var fs = require("fs");
var zlib = require('zlib');

// 压缩 input.txt 文件为 input.txt.gz
fs.createReadStream('input.txt')
  .pipe(zlib.createGzip())
  .pipe(fs.createWriteStream('input.txt.gz'));
  
console.log("文件压缩完成。");
```

代码执行结果如下：

```
$ node compress.js 
文件压缩完成。
```

##### 链式流(解压文件)

```js
var fs = require("fs");
var zlib = require('zlib');

// 解压 input.txt.gz 文件为 input.txt
fs.createReadStream('input.txt.gz')
  .pipe(zlib.createGunzip())
  .pipe(fs.createWriteStream('input.txt'));
  
console.log("文件解压完成。");
```

代码执行结果如下：

```
$ node decompress.js 
文件解压完成。
```



## 1.3 Node.js模块系统

##### 所属作者: 

​	[菜鸟教程 node 模块系统](https://www.runoob.com/nodejs/nodejs-module-system.html)



### 1.3.1 require 模块的执行顺序

![img](https://www.runoob.com/wp-content/uploads/2014/03/nodejs-require.jpg)





## 1.4 文件系统 fs

##### 所属作者: 

​	[菜鸟教程 node 文件系统](https://www.runoob.com/nodejs/nodejs-fs.html)

### 1.4.1 打开文件



### 语法

以下为在异步模式下打开文件的语法格式：

```js
fs.open(path, flags[, mode], callback)
```

### 参数

参数使用说明如下：

- **path** - 文件的路径。
- **flags** - 文件打开的行为。具体值详见下文。
- **mode** - 设置文件模式(权限)，文件创建默认权限为 0666(可读，可写)。
- **callback** - 回调函数，带有两个参数如：callback(err, fd)。

flags 参数可以是以下值：

| Flag | 描述                                                   |
| :--- | :----------------------------------------------------- |
| r    | 以读取模式打开文件。如果文件不存在抛出异常。           |
| r+   | 以读写模式打开文件。如果文件不存在抛出异常。           |
| rs   | 以同步的方式读取文件。                                 |
| rs+  | 以同步的方式读取和写入文件。                           |
| w    | 以写入模式打开文件，如果文件不存在则创建。             |
| wx   | 类似 'w'，但是如果文件路径存在，则文件写入失败。       |
| w+   | 以读写模式打开文件，如果文件不存在则创建。             |
| wx+  | 类似 'w+'， 但是如果文件路径存在，则文件读写失败。     |
| a    | 以追加模式打开文件，如果文件不存在则创建。             |
| ax   | 类似 'a'， 但是如果文件路径存在，则文件追加失败。      |
| a+   | 以读取追加模式打开文件，如果文件不存在则创建。         |
| ax+  | 类似 'a+'， 但是如果文件路径存在，则文件读取追加失败。 |

### 实例

接下来我们创建 file.js 文件，并打开 input.txt 文件进行读写，代码如下所示：

```js
var fs = require("fs");

// 异步打开文件
console.log("准备打开文件！");
fs.open('input.txt', 'r+', function(err, fd) {
   if (err) {
       return console.error(err);
   }
  console.log("文件打开成功！");     
});
```

以上代码执行结果如下：

```
$ node file.js 
准备打开文件！
文件打开成功！
```



## 1.5  Node.js Express 框架

##### 所属作者: 

​	[菜鸟教程 node Express](https://www.runoob.com/nodejs/nodejs-express-framework.html)



### 1.5.1  静态文件

Express 提供了内置的中间件 **express.static** 来设置静态文件如：图片， CSS, JavaScript 等。

你可以使用 **express.static** 中间件来设置静态文件路径。例如，如果你将图片， CSS, JavaScript 文件放在 public 目录下，你可以这么写：

```
app.use('/public', express.static('public'));
```

我们可以到 public/images 目录下放些图片,如下所示：

```
node_modules
server.js
public/
public/images
public/images/logo.png
```

让我们再修改下 "Hello World" 应用添加处理静态文件的功能。

创建 express_demo3.js 文件，代码如下所示：

## express_demo3.js 文件代码：

```js
var express = require('express');
var app = express();
 
app.use('/public', express.static('public'));
 
app.get('/', function (req, res) {
   res.send('Hello World');
})
 
var server = app.listen(8081, function () {
 
  var host = server.address().address
  var port = server.address().port
 
  console.log("应用实例，访问地址为 http://%s:%s", host, port)
 
})
```



执行以上代码：

```
$ node express_demo3.js 
应用实例，访问地址为 http://0.0.0.0:8081
```

执行以上代码：

在浏览器中访问 http://127.0.0.1:8081/public/images/logo.png