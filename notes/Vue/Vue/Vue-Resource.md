---
title: Vue-Resource
date: 2019-08-09 11:16:07
tags: Vue全家桶
categories: Web前端开发
---

```
vue-resource
JSONP实现原理:
	1)由于浏览器的安全性限制,不允许AJAX访问协议不同,域名不同,端口号不同的数据接口,浏览器认为这种访问是不安全的;
	2)可通过动态创建script标签的形式,把script标签的src属性,指向数据接口的地址,因为script标签不存在跨域限制,这种数据获取方式,称作JSONP(注意: 根据JSONP的实现原理知晓,JSONP只支持Get请求);
	3)具体实现过程:
		先在客户端定义一个回调方法,预定义对数据的操作,再把这个回调方法的名称,通过URL传参的形式,提交到服务器的数据接口,服务器数据接口组织好要发送给客户端的数据,再拿着客户端传递过来的回调方法名称,拼接出一个调用这个方法的字符串,发送给客户端去解析执行,客户端拿到服务器返回的字符串之后,当作Script脚本去解析执行,这样就能够拿到JSONP的数据了;
------------------------------------------------------------------------
发送get请求:
getInfo() {
  this.$http.get('http://127.0.0.1:8899/api/getlunbo').then(res => {
    console.log(res.body);
  })
}
--------------------------------------------------------------------
发送post请求:
postInfo() {
  var url = 'http://127.0.0.1:8899/api/post';
  // post 方法接收三个参数:
  // 参数1: 要请求的URL地址
  // 参数2: 要发送的数据对象
  // 参数3: 指定post提交的编码类型为 application/x-www-form-urlencoded
  this.$http.post(url, {}, { emulateJSON: true }).then(res => {
    console.log(res.body);
  });
}
---------------------------------------------------------
发送JSONP请求获取数据:
jsonpInfo() { // JSONP形式从服务器获取数据
  var url = 'http://127.0.0.1:8899/api/jsonp';
  this.$http.jsonp(url).then(res => {
    console.log(res.body);
  });
}
--------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <title>Document</title>
   <script src="./vue.js"></script>
   <script src="https://cdn.jsdelivr.net/npm/vue-resource@1.5.1"></script>
   <!-- 注意: vue-resource依赖于Vue,注意先后顺序,vue-resource会在vue上注册一个 $http -->
</head>
<body>
   <div id="app">
      <input type="button" value="get请求" @click="getInfo">
      <input type="button" value="post请求" @click="postInfo">
      <input type="button" value="jsonp请求" @click="jsonpInfo">
   </div>
   <script>
      var vm = new Vue({
         el: '#app',
         methods: {
            getInfo() {
               // 发起get请求:
               // this.$http.get('url',[options]).then(successCallback, errorCallback)
               // 以后看到.then就应该想到它是用promise封装的,回调有成功回调和失败回调,成功回调是必须的,[options]和失败回调都是可以省略的
               this.$http.get('http://www.liulongbin.top:3005/api/getlunbo').then(function(result) {
                  //通过result.body拿到服务器返回的成功数据
                  console.log(result.body)
               })
            },
            postInfo() {
               // 发起post请求: application/x-www-form-urlencoded
               // this.$http.post('url',[body],[options]).then(successCallback, errorCallback);
               // 手动发起post请求,默认没有表单格式,导致有的服务器处理不了,通过post方法的第三个参数,emulateJSON:true设置提交的内容类型为普通表单数据格式即可;
               // (参数): 地址 要提交给服务器的数据 以普通表单的形式提交给服务器的
               this.$http.post('http://www.liulongbin.top:3005/api/post', {}, {emulateJSON:true}).then(result=>{
                  console.log(result.body)
               })
            },
            jsonpInfo() {
               // 这是发起JSONP请求
               this.$http.jsonp('http://www.liulongbin.top:3005/api/Jsonp').then(result => {
                  console.log(result.body)
               })
            }
         }
      })
   </script>
</body>
</html>
```
