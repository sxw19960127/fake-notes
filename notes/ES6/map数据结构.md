`json`数据结构：

```js
let json = {
    name: 'sxw',
    skill: 'eat'
};
console.log(json.name) 
// 这种方法是要遍历所有的,速度要比数组的慢,灵活性不好;
```

`map`数据结构：

```js
var map = new Map();
map.set(json, 'I am');						// key值		=>	value值
console.log(map);// Map{Object {name: 'sxw',skill: 'eat'} => "I am"}
map.set('sxw',json); 
console.log(map); //这个时候,字符串就变成了key值,json对象就变成了value值了
```

`map`的增删查

```js
// 取值
console.log(map.set(json)); //I am,取出key值是json的值
console.log(map.set('sxw'))
```

```js
// 删值
map.delete(json); // 删除指定key
console.log(map);

// 删除所有
map.clear();

// 查看当前还有几个值
console.log(map.size);

// 查找
console.log(map.has('sxw')) //查找key值为'sxw'的,有则返回true,没有则返回false
```

