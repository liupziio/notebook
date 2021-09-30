

参考文档 : http://nodejs.cn/api/path.html



- path.basename
  - 获取路径的文件名(默认包括拓展名)
  - 第二个参数path.basename('c:/aa/bb/cc/lpz.js','.js') 得到lpz去除掉后缀名.js
- path.dirname
  - 获取一个路径中的路径部分
  - path.dirname('c:/aa/bb/cc/lpz.js','.js') 得到c:/aa/bb/cc/
- path.extname
  - 获取一个路径的拓展名部分
  - path.basename('c:/aa/bb/cc/lpz.js')得到 .js
- path.parse
  - 把一个路径转为对象
    - root : 根路径
    - dir : 目录
    - base : 包含后缀名的文件名
    - ext : 后缀名
    - name : 不包含后缀名的文件名
- path.join
  - 当你需要路径拼接用这个方法
  - path.join("a" + "b"+"c") 得到 a\b\c
  - path.join("a" ,"b","c") 得到 a\b\c
- path.isAbsolute
  - 判断一个路径是否是绝对路径