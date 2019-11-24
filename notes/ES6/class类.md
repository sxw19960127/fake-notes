```js
class Coder{
    // 类里面都是函数方法
    name(val) {
        console.log(val);
        return val; // 切记要 return,否则是 undefined
    }
    // 注意: 多方法声明的时候,方法与方法之间不用加逗号
    skill(val) {
        console.log(this.name('舒小伟') + ':' + 'skill' + val)
    }
    
    // 给类进行传参,使用 constructor 进行类的参数的设置
    constructor(a,b) {
        this.a = a;
        this.b = b;
    }
    
    add() {
        return this.a + this.b
    }
}
// 步骤1,2
let sxw = new Coder;
// sxw.name('舒小伟');
sxw.skill('web')

// 步骤3
// 给类进行传参
let sxw = new Coder(1,2);
console.log(sxw.add())
```

类的继承

```js
class htmler extend Coder{
    
}

let kobe = new htmler;
// kobe调用了父类Coder中的方法
kobe.name('书宣');
```

