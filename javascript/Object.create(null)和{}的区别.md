#### Object.create(null)和{}的区别
```
    var obj = Object.create(null)
    Object.create(null)创建出来的对象为干净的map，没有附加其他属性

    var obj = {}
    字面量{}创建出来的对象，其原型指向Object.prototype，也就是 obj.__proto__ === Object.prototype，同时包含了toString,hasOwnProperty等方法。

```

#### 手写Object.create
```
    // create并不是在原型上的，直接判断是否有这个方法
    if (typeof Object.create !== "function") {
        Object.create = function(proto, properties) {
            // 判断类型，第一个参数传入的必须是 object, function
            if (typeof proto !== "object" && typeof proto !== "function") {
                throw new TypeError("Object prototype may only be an Object: " + proto);
            } 
            // 这个判断可有可无，至少在chrome中是允许传入null的
            // else if (proto === null) {
            //   throw new Error(
            //     "This browser's implementation of Object.create is a shim and doesn't support 'null' as the first argument."
            //   );
            // }

            // 简单的实现的过程，忽略了properties
            var func = function() {};
            func.prototype = proto; // 将fn的原型指向传入的proto
            return new func();  // 返回创建的新对象，这里思考下，new func() 又做了什么事情呢？且往下看！
        };
    }


    new func()做了什么?
    new func()的作用是创建一个新的对象，其中func是一个构造函数，在这个过程中，主要包含了如下步骤：

    1. 创建空对象obj;
    2. 将obj的原型设置为构造函数的原型，obj.__proto__= func.prototype;
    3. 以obj为上下文执行构造函数，func.call(obj);
    4. 返回obj对象。

```

#### 手写new
```
    function objectCreator(func) {
        // 创建一个空对象，并将空对象的原型设置为构造函数的原型
        var obj = Object.create(func.prototype);
        // 以obj为上下文执行构造函数
        var newObj = func.call(obj);
        // 如果构造函数有返回结果，则返回，若无直接返回obj
        if (typeof newObj == "object") {
            return newObj;
        } else {
            return obj;
        }
    }
```