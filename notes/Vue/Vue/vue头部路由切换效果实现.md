---
title: vue头部路由切换效果实现
date: 2019-09-06 14:53:04
tags:
---

2019/9/6

```
描述: 在单页面应用中,通过点击路由实现页面跳转功能,给跳转添加一个样式,有更好的用户体验;
```

```
router.js
import Header from './components/Header.vue'
import Footer from './components/Footer.vue'
routes: [
    {path: '/',component: Header},
    {path: '/header', component: Header},
    {path: '/footer', component: Footer}
]
```

```
App.vue
<router-link v-for="item in lists" :key="item.url" :to="item.url">
    <div :class="flag === item.url ? 'selected' : ''">
    	{{ item.name }}
    </div>
</router-link>
<router-view></router-view>
---------------------------
<script>
export default {
  data() {
    return {
      lists: [
        {
          url: '/header',
          name: '头组件'
        },
        {
          url: '/footer',
          name: '尾组件'
        }
      ],
      flag: ''
    }
  },
  watch: {	//监听,什么在变化？当我们点击的时候路由地址url在变化！
    '$route.fullPath': function(newVal) { //获取变化了的新的url地址 === newVal
      console.log(newVal)
      this.flag = newVal //讲值赋予 flag
    }
  }
}
</script>
-----------------------------------------
<style style="scss" scoped>
  .selected{
    background-color: red;
    width: 200px;
    height: 200px;
  }
</style>
```

wow.js的使用方法

<https://www.cnblogs.com/sese/p/5630454.html>

animate.js的使用方法

<https://www.cnblogs.com/xiaohuochai/p/7372665.html>