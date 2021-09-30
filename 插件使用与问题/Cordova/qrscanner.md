# 插件状态值

+ authorized
  + 布尔值
  + 摄像头允许时候为 **true**
+ denied
  + 布尔值
  + 拒绝摄像头为 **true**
+ restricted
  + 布尔值
  + 其他原因,无法获取到授权时为 **true**
+ prepared
  + 布尔值
  + 把视频给客户看时为 **true**
+ showing
  + 布尔值
  + 当预览可见时为 **true** (并且web视图背景色变为透明)
+ scanning
  + 布尔值
  + 扫描到了二维码数据才为 **true**
+ previewing
  + 布尔值
  + 当QRScanner显示设备摄像头的实时预览时为真。当预览暂停时设置为false。
+ lightEnabled
  + 布尔值
  + 当手电筒亮时为 **true**
+ canOpenSettings
  + 布尔值
  + ...
  + *：*只有当用户的操作系统能够使用qrscann. opensettings()时，这才是正确的。
+ canEnableLight
  + 布尔值
  + 客户的手电筒 **可以** 亮才为 **true**
+ canChangeCamera
  + 布尔值
  + 仅当当前设备“应该”有前置摄像头时为真。摄像机可能仍然无法捕获，当尝试切换时，将发出错误代码3、4或5。(在浏览器平台上，这个值是假的，直到prepare方法被调用。)
+ currentCamera
  + number
  + 后置摄像头为 0 前置摄像头为 1