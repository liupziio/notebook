#### 获取访问我那个机器的IP地址与端口号

------

###### req.socket.remoteAddress获取到IP地址

######  req.socket.remotePort获取到端口号

// ip 地址用来定位计算机
// 端口号用来定位具体的应用程序
// 所有需要联网通信的应用程序都会占用一个端口号

```js
server.on('request', function (req, res) {
  //console.log('收到请求了，请求路径是：' + req.url)
  #console.log('请求我的客户端的地址是：', req.socket.remoteAddress, req.socket.remotePort)

  res.end('hello nodejs')
})
```

