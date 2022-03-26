# WebViewScriptBridge
ios与js交互
在 main.js 中引入该文件

import Bridge from './config/bridge.js'
Vue.prototype.$bridge = Bridge
在需要调用客户端方法的组件中（事先需要与客户端同事约定好方法名，ObjC Echo是VUE端往APP端传值的方法）

// params是向app端传的参数
// iOS端
this.$bridge.callhandler('ObjC Echo', params, (data) => {
    // 处理返回数据
});
 
 
// Android端
JSAndroid.requestPaySupportWithPayWay(params);
当客户端需要调用 js 函数时,在mounted钩子中事先注册约定好的函数即可（JS Echo是APP端返回值给VUE端的调用方法名称）

// iOS端
this.$bridge.registerhandler('JS Echo', (data, responseCallback) => {
  alert('JS Echo called with:', data)
  responseCallback(data)
});
 
// Android端
window['JS Echo'] = (data, responseCallback) => {
   alert('JS Echo called with:', data)
   responseCallback(data)
}
