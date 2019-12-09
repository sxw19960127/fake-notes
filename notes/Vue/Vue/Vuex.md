---
title: Vuex
date: 2019-08-08 20:28:28
tags: Vue全家桶
categories: Web前端开发
---

```
VueX状态管理系统
npm install vuex
---------------------------------
store.js中
import Vue from "vue"
import Vuex from "vuex"
Vue.use(Vuex)
export default new Vuex.Store({
   state: {
      count: 0
   }
})
--------------------------------
main.js中:
import store from './store.js'
new Vue({
   store: store //注册一下
})
-------------------------------------------
组件中获取数据:
<script>
   export default{
      computed: {
         count() {
            return this.$store.state.count
         }
      }
   }
</script>
```

```
getters属性:
作用: 当我们在不同组件中操作相同数据(对数据的运算也一样时),我们可以把它提取出来;
	 或者当我们处理从后台传过来的数据,也可以在getters里面进行操作;
import Vue from "vue"
import Vuex from "vuex"
Vue.use(Vuex)
export default new Vuex.Store({
   state: {
      count: 0
   },
   getters: { //作用和计算属性相似,只要检测到state发生变化,立即执行函数return出最新的数值
      doubleCount(state) {
         return state.count * 2;
      }
   }
})
在需要进行运算处理的函数中获取使用数值:
return this.$store.getters.doubleCount; //写在计算属性里面的,主要state数值发生变化立即会进行更新
```

```
vuex是状态管理系统,要追踪数据,所以我们不允许在组件中进行数据的加减,只能如下进行数据的变动:
import Vue from "vue"
import Vuex from "vuex"
Vue.use(Vuex)
export default new Vuex.Store({
   state: {
      count: 0
   },
   getters: { 
      doubleCount(state) {
         return state.count * 2;
      }
   },
   mutations: { //只允许将数据的变动函数写在这个里面,不允许有异步操作
      increaseCount(state) {
         state.count ++;
      },
      decreaseCount(state) {
         state.count --;
      }
   }
})
-------------------------------------------------------
在组件中怎么去调用这个定义好的函数呢？
// 逻辑处理部分 this.$store.commit("increaseCount")
-------------------------------------------
export default new Vuex.Store({
   state: {
      count: 0
   },
   getters: { 
      doubleCount(state) {
         return state.count * 2;
      }
   },
   mutations: { 
      increaseCount(state) {
         state.count ++;
      },
      decreaseCount(state) {
         state.count --;
      }
   },
   actions: { //这里可以写异步操作
      actionsIncrease(context) {
         console.log(context)
         setTimeout(() => {
            context.commit("increaseCount", 5)
         }, 1000)
      }
   }
})
------------------------------------------------
调用: this.$store.dispatch("actionsIncrease")
```

```
辅助函数: 简化我们获取数据等操作:
<script>
   import {mapState,mapGetters} from "vuex"
   export default {
      computed: {
         ...mapState(["count","value"]), //获取state中的count值和value值
         ...mapGetters(["doubleCount"]),
      }
   }
</script>
...
<script>
   import {mapMutations,mapActions} from "vuex"
   export default {
      methods: {
         ...mapActions(["actionsIncrease"]),
         ...mapMutations(["decreaseCount"])
      }
   }
</script>
```
