# 安装

1. 安装electron失败 postinstall: node install.js

```shell
解决方法：将electron下载地址指向taobao镜像

npm config set electron_mirror "https://npm.taobao.org/mirrors/electron/"
```

# error

## 打包时报错误

```js
npm run electron:build
```



```js
  • "electron-squirrel-startup" dependency is not required for NSIS
  • packaging       platform=win32 arch=x64 electron=6.0.0 appOutDir=dist_electron\win-unpacked
  • asar using is disabled — it is strongly not recommended  solution=enable asar and use asarUnpack to unpack files that must be externally available
  • file source doesn't exist  from=D:\electron-vue-demo\resources
  • default Electron icon is used  reason=application icon is not set
  ⨯ Get https://github.com/electron-userland/electron-builder-binaries/releases/download/winCodeSign-2.5.0/winCodeSign-2.5.0.7z: read tcp 192.168.18.202:60743->52.74.223.119:443: wsarecv: A connection attempt failed because the connected party did not properly respond after a period of time, or established connection failed b
```

解决方案:

+ 设置electron镜像。

```js
	npm config edit
```

使用该命令会弹出npm的配置文档，将以下类容复制到文件末尾。

```js
electron_mirror=https://npm.taobao.org/mirrors/electron/
electron-builder-binaries_mirror=https://npm.taobao.org/mirrors/electron-builder-binaries/

```

