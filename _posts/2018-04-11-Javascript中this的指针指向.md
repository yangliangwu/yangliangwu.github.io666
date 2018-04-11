# 一、什么是this指针？

在`Javascript`中，`this`指针是指在创建函数时，由系统默认生成的两个隐式参数之一（另一个是`arguments`)。

# 二、this指针指向哪？
### 有以下四种情况：

1. 作为函数进行调用，浏览器中this指向window对象，node中this指向global对象。
2. 当函数作为方法的形式调用时，this指向方法的拥有者。

例如：
```javascript
var a = 'outer'
var obj = {
  a: 'inner',
  foo: function () { // 作为方法调用，obj对象的foo
    function test () { // 作为函数调用
      console.log(this.a) // 输出outer，说明此处
    }
    test()
    console.log(this.a) // 输出inner
  }
}

obj.foo() // 调用obj对象的foo方法

```
3. 在构造器中

```javascript
  function Person (name, age) {
    this.name = name;
    this.age = age;
    this.introduce = function () {
      console.log('I am ' + this.name + ', ' + this.age + ' years old.')
    }
  }
  
  var Byron = new Person('Byron', 25) // 新建一个对象，构造器的this指针指向该对象。Person作为类，Byron作为实例。
  
  Byron.introduce() // 输出 I am Byron, 25 years old.
  
```

4. 在`call()` 和 `apply()`中调用

    在`call()`和`apply()`方法中调用，我们可以自定义this指针的指向。
