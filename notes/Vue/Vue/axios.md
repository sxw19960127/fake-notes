---
title: axios
date: 2019-08-08 15:14:27
tags: Vue全家桶
categories: Web前端开发
---

```
axios连接服务器,发送ajax请求
---------------------------
npm install axios --save 
---------------------------
firebase 免费提供数据库,提倡前端不需要后端直接操作数据库,适合创业公司的理念;
-----------------------------------------------------------------
发送数据:
axios.post(第一个参数是请求地址,第二个参数请求头(选填),第三个参数是数据)
     .then( res => {
        console.log(res)
     }, (err) => {
        console.log(err)
     })
-----------------------------------
获取数据:
<script>
   import axios from "axios"
   export default{
      data() {
         return {
            email: ''
         }
      }
   },
   created() {
      axios.get(第一个参数是获取数据的地址,第二个参数是请求头配置项(选填))
            .then( data => {
                  // 处理数据
                  // console.log(data)
                  const arr = [];
                  for(let key in data.data) {
                     let myData = data.data[key];
                     myData.id = key;
                     arr.push(myData);
                  }
                  this.email = arr[i].email
            }, err => {

            })
      }
</script>
-----------------------------------
全局进行配置项:
由于局部进行配置项只要在第二个参数中使用对象的形式就行了,这里主要来进行全局配置的讲解:
在main.js中:
import axio from 'axios'
axios.defaults.baseURL = "https://www..." //全局配置请求地址
axios.defaults.headers.common["Accept"] = "application/json" 
//这里可以单独进行get的配置和post的配置,我们使用common进行通用配置,请求头 ['Accept'],接收什么样的数据,要接收一个 application/json json形式的数据 /在浏览器的Network中显示: Accept:application/json
axios.defaults.headers.post["Authorization"] = "123"
--------------------------------------------------------
拦截器:
(将请求拦截掉): 
axios.interceptors.request.use( config => {
   console.log(config)
   console.log("loading")
   // 相关逻辑操作,像加loading...
   return config //必须要return,不然请求信息不会显示出来,一直存在被拦截状态
})
(将返回的数据在页面呈现前拦截掉):
axios.interceptors.response.use( data => {
   console.log(data.status === "404")
   //这里有一个status状态码,我们可以根据返回的状态码进行相关处理操作,像弹出一个alert框,提示用户信息出错去联系管理员...
   return data //同样要进行return 操作
})
-------------------------------
创造额外的axios实例: 用来解决请求的链接地址比较多的情况
配置两份不同的请求:
axios.js里:
import axios from "axios";
const instance = axios.create()
instance.defaults.baseURL = "https://www..." //不一样的请求地址
export default instance
用法和之前的一样!
```

