`proxy`代理，增强对象和函数。

```js
let obj = {
    add: function(val) {
        return val + 100
    },
    name: 'I am sxw'
}
console.log(obj.add(100));
console.log(obj.name);
```

使用`proxy`代理：

```js
let pro = new Proxy({
    add: function(val) {
        return val + 100;
    },
    name: 'I am sxw'
},{
    // 预处理机制 get set apply
    
    // get表示在得到某个属性之前进行处理,第三个参数可以省略
    get: function(target,key,property) {
        console.log('come in Get');
        console.log(target)
        console.log(key)
        return target[key] //加上这一行代码,程序就会既输出预处理机制中的内容,也会输出我们想让其输出的目标内容
    }
    set: function(target,key,value,receiver) {
    	console.log(` setting ${key} = ${value} `); // setting name = 舒小伟
    	return target[key] = value; // 记住,我们预处理完成的结果一定要返回,才能生效
	}
})
console.log(pro.name) // 在这里我们调用pro的name方法,程序是会走进get预处理机制里面

pro.name = '舒小伟'
console.log(pro.name)
```



`apply`：代理方法

```js
let target = function() {
    return 'I am sxw';
}
let handle = {
    apply(target,ctx,args) {
        console.log('do apply')
        return Reflect.apply(...arguments);
    }
}
let pro = new Proxy(target, handle);
console.log(pro())
```

