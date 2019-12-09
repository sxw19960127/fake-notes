```html
<!DOCTYPE html>
<html lang="en">
<head>
   <meta charset="UTF-8">
   <meta name="viewport" content="width=device-width, initial-scale=1.0">
   <meta http-equiv="X-UA-Compatible" content="ie=edge">
   <title>Document</title>
</head>
<body>
   <div id="app">
      <!-- 观察下面这连个span，可以发现他们结构是差不多的，所以vue底层的虚拟dom会将其中一份作为备份，当条件不满足的时候显示另一份的时候，并不会重新创建另一个span结构，而是从虚拟dom中拿，只是更改了简单的id等属性，但是内容并不会去修改她，所以这样就会造成一个bug，当在用户账号中输入一些内容的时候，切换到用户邮箱的时候，哪些内容依旧存在，解决方法就是加key值，只要是key值不同，虚拟dom就知道这两个不是相同的结构了。还有下面的label中的for对应下面input中的id，这样的好处就是当点击用户账号的时候,就回去找对应的input框 -->
       // 复用
      <span v-if="isUser">
         <label for="username">用户账号</label>
         <input type="text" id="username" placeholder="用户账号" key="username">
      </span>
      <span v-else>
         <label for="email">用户邮箱</label>
         <input type="text" id="email" placeholder="用户邮箱" key="email">
      </span>
      <button @click="isUser = !isUser"></button>
   </div>
   <script>
      const app = new Vue({
         el: '#app',
         data: {
            isUser: true
         }
      })
   </script>
</body>
</html>
```

```html
// set(要修改的对象, 索引值, 修改后的值) --- 功能类似于 数组的splice方法
Vue.set(this.letters, 0, 'aaa')

// 注意：通过索引值去修改数组中的元素不是响应式的
this.letters[0] = 'aaa'; // 真实中数组中的数据是被修改了的，但是vue没有实时监听这个方法，页面并不会被渲染起来
```

