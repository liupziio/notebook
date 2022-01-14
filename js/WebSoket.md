```js
var webSoket = null;
var timer = null;
// var requestNum = 0;
// var timerLength = 2000;
var resetFlag = 0;
var resetLength = 500;
var resetTimer = null;
var lockReconnect = false; //避免重复连接
var closeFlag = 0;
import store from "../store";
const initWebSocket = function () {
  // console.log(store.state.websoketStore.data);
  if (typeof WebSocket === "undefined") {
    console.log("您的浏览器不支持WebSocket");
  } else {
    const wsurl = "ws://192.168.1.165:8081/webSocket/" + "A-" + JSON.parse(localStorage.getItem("user")).userId;
    // 实例化 WebSocket
    webSoket = new WebSocket(wsurl);
    console.log(webSoket);
    // 监听 WebSocket 连接
    webSoket.onopen = websocketonopen;
    // 监听 WebSocket 错误信息
    webSoket.onerror = websocketonerror;
    // 监听 WebSocket 消息
    webSoket.onmessage = websocketonmessage;
    // 关闭WebSocket
    webSoket.onclose = websocketclose;
  }
};
// 连接建立之后执行send方法发送数据
const websocketonopen = function () {
  console.log("socket连接成功");
  start();
};
// 连接建立失败重连
const websocketonerror = function (e) {
  console.log("连接错误");
  console.log(e);
  // reset();
  // initWebSocket();
};
// 数据接收
const websocketonmessage = function (e) {
  start();
  //   console.log(requestNum, "接收");
  console.log(e);
  const resdata = JSON.parse(e.data);
  if (resdata.code === 200) {
    // store.commit("websoketStore/saveSoketData", resdata.data);
    store.dispatch("websoketStore/setUserActions", resdata.data);
  }
  if (resdata.code === 201) {
    websocketsend(JSON.stringify({ type: "refresh", userId: "A-" + JSON.parse(localStorage.getItem("user")).userId }));
  }
  if (resdata.code === 202) {
    // store.commit("websoketStore/saveSoketData", resdata.data);
    store.dispatch("websoketStore/setUserActions", resdata.data);
  }
};
// 数据发送
const websocketsend = function (Data) {
  console.log(Data);
  webSoket.send(Data);
};
// 关闭
const websocketclose = function (e) {
  console.log("WebSocket 断开连接", e);
  if (closeFlag === 1) {
    return;
  }
  console.log("开始");
  reset();
};
// 断开重连
const reset = function () {
  resetLength = resetLength * 1.5;
  resetTimer && clearTimeout(resetTimer);
  // if (closeFlag === 1) {
  //   return;
  // }
  if (lockReconnect || resetFlag > 5) {
    return;
  }
  lockReconnect = true;
  resetFlag += 1;
  resetTimer = setTimeout(() => {
    initWebSocket();
    lockReconnect = false;
  }, resetLength);
};
//心跳包
const start = function () {
  timer && clearTimeout(timer);
  timer = setTimeout(() => {
    websocketsend("1");
  }, 2000);
};
const close = function () {
  closeFlag = 1;
  webSoket.close();
};

export default {
  webSoket,
  initWebSocket,
  websocketsend,
  websocketclose,
  close,
};
```

