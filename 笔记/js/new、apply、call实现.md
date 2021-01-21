### 手动实现new、apply、call、bind

#### new实现

##### new方法做了些什么

1. 生成一个新对象
2. 新对象继承构造方法原型属性
3. 执行构造函数，改变this指向，指向新对象
4. 如果构造函数return了对象类型或函数类型，new出来的就是构造函数返回的
##### 代码
```javascript
function _new (ctor, ...args) {
    // 判断入参
    if (typeof ctor !== 'funciton') {
        console.error(new Error('ctor must be a funciton'))
        return
    }
    // 生成新的对象
    const obj = new Object()
    // 改变新对象原型链
    obj.__proto__ = ctor.prototype
    // 执行构造函数,使用apply改变this指向
    const res = ctor.apply(obj, args)
    const isObject = typeof res === 'object' && res !== null
    const isFunction = typeof res === 'function'
    // 判断构造函数有返回的情况
    return (isObject || isFunction) ? res : obj
}
```

#### call实现
##### call做了什么
call函数的调用者是需要改变指向的`函数本身`
1. 将需要执行的函数挂载到目标上下文(目标this)上
2. 执行复制的函数
3. 返回
##### 实现
```javascript
Function.prototype._call = function (context, ...args) {
    context = context || window
    // 复制函数
    context._call_interim_fn = new Function(`return ${this}`)()
    // 执行
    const result = context._call_interim_fn(...args)
    // 删除临时属性
    delete context._call_interim_fn
    return result
}
```

#### apply实现
apply和call唯一差别就是参数的处理
##### 实现
```javascript
Function.prototype._apply = function (context, args = []) {
    context = context || window
    context._apply_interim_fn = new Function(`return ${this}`)()
    const result = context._apply_interim_fn(...args)
    delete context._apply_interim_fn
    return result
}
```

#### bind实现
bind的区别在于，不立即执行，而是把复制的函数封装返回
```javascript
Function.prototype._bind = function (context, ...args) {
    context = context || window
    context._bind_interim_fn = new Function(`return ${this}`)()
    return function() {
        const result = context._bind_interim_fn(args)
        delete context._bind_interim_fn
        return result
    }
}
```