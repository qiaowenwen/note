##this 的指向问题

**JS 中 this 的指向不同于其他语言，JS 中的 this 不是指向定义他的位置，而是在哪调用它它就指向哪里。**

在 js 中函数的调用方式有三种：直接调用、函数调用、方法调用。除此之外还有一些特殊的调用。比如使用 bind()将函数绑定后调用，或者使用 call 和 apply 等方法。在 es6 引入了箭头函数之后，this 的指向又发生了变化，具体的问题具体分析

> <font color="#0000dd">直接调用</font><br />

直接调用指的是使用函数名(...)的调用方式，这时候函数内部的 this 就是指向全局对象 window。

```js
function test() {
  console.log(this === window) // true
}
test() // 直接调用
```

**注意**：直接调用不是指在全局中的调用，其实指的是在任何的作用域下都可以进行的调用的方式。

```js
;(function() {
  function test() {
    console.log(this === window) // true
  }
  test() // 非全局作用域下的直接调用
})()
```

```js
const obj = {}
function test() {
  console.log(this, this == obj) //window false
  return this == obj
}
console.log(test(), '9') // false
```

> <font color="#0000dd">方法调用</font><br />

方法调用是指通过对象来调用其方法函数，它是 对象.方法函数(...) 这样的调用形式。这种情况下，函数中的 this 指向调用该方法的对象。但是，同样需要注意 bind() 的影响。

```js
// 第一种方式，定义对象的时候定义其方法
const obj = {
  test() {
    console.log(this === obj) // true
  }
}
obj.test()

// 第二种方式，对象定义好之后为其附加一个方法(函数表达式)
obj.test2 = function() {
  console.log(this === obj) //true
}
obj.test2()

// 第三种方式和第二种方式原理相同
// 是对象定义好之后为其附加一个方法(函数定义)
function t() {
  console.log(this === obj) //true
}
obj.test3 = t
obj.test3()
```

> <font color="#0000dd">new 调用</font><br />

在 es6 之前，任何函数可以当做是构造函数，通过 new 产生新的对象，也称为实例化对象。而其中的 this 就指向这个新对象。这没有什么悬念，因为 new 本身就是设计来创建新对象的。

```js
function AClass(data) {
  console.log(this)
  this.data = data
}

var a = new AClass('Hello World')
console.log(a.data) // Hello World
console.log(data) // Hi

var b = new AClass('Hello World')
console.log(new AClass('Hello World'))
console.log(a === b) // false
```

##特殊情况下 this 的指向问题

> <font color="#0000dd">箭头函数</font><br />

前面介绍了，除了通常情况下的 this 的指向问题，接下来介绍特殊情况下 this 的指向的问题。

示例中的两个 this 都是由箭头函数的直接外层函数(方法)决定的，而方法函数中的 this 是由其调用方式决定的。上例的调用方式都是方法调用，所以 this 都指向方法调用的对象，即 obj。

箭头函数让大家在使用闭包的时候不需要太纠结 this，不需要通过像 \_this 这样的局部变量来临时引用 this 给闭包函数使用。来看一段 Babel 对箭头函数的转译可能能加深理解：

```js
const obj = {
  test() {
    const arrow = () => {
      // 这里的 this 是 test() 中的 this，
      // 由 test() 的调用方式决定
      console.log(this === obj)
    }
    arrow()
  },

  getArrow() {
    return () => {
      // 这里的 this 是 getArrow() 中的 this，
      // 由 getArrow() 的调用方式决定
      console.log(this === obj)
    }
  }
}

obj.test() // true
const arrow = obj.getArrow()
arrow() // true
```

> <font color="#0000dd">call、apply、bind</font><br />

call 和 apply 以及 bind 都能改变 this 的指向但是，bind 的优先级相对较高

```js
const obj = {}
function test() {
  console.log(this === obj)
}

// 绑定到一个新对象，而不是 obj
const testObj = test.bind({})
test.apply(obj) // true
// 期望 this 是 obj，即输出 true
// 但是因为 testObj 绑定了不是 obj 的对象，所以会输出 false
testObj.apply(obj) // false
```

https://www.cnblogs.com/wxtlinlin/p/6523950.html
https://www.cnblogs.com/long-long/p/6741083.html
