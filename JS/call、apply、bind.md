# 手写call、apply、bind函数

------

#### 手写call函数：

```javascript
// 手写call函数
Function.prototype.call1 = function (obj, ...args) {
  // 保存传入的this
  const context = obj
  // 避免覆盖原来的方法，所以就使用Symbol保证唯一性
  const fn = Symbol()
  // 把方法添加到传入的this，然后方法指向call1的调用者this
  context[fn] = this
  // 执行方法
  const result= context[fn](...args)
  // 删除传入this的fn方法
  delete context[fn]
  // 返回结果
  return result
}
```

```javascript
//简单的使用
function sum(num1,num2){
  console.log(this.base + num1+num2 )
}
const obj={
  base:1,
}
sum.call(obj,10,20)
// 结果为31
```

手写apply方法：

```javascript
Function.prototype.apply1 = function (obj, args) {
  //相较于call函数，apply对于传参并不是依次传参，而是以数组的形式
  const context = obj
  const fn = Symbol()
  context[fn] = this
  const result = context[fn](...args)
  delete context[fn]
  return result
}
```

```js
//简单的使用
function sum(num1, num2) {
  console.log(this.base + num1 + num2)
}
const obj = {
  base: 1,
}
sum.apply1(obj, [10, 20])
// 结果为31
```

手写bind函数：

```js
// 手写bind函数
Function.prototype.mybind = function (This, ...outherArgs) {
  // 缓存调用函数
  const thatFunc = this
  const fBind = function (...innerArgs) {
    // 判断是否是new还是直接执行函数
    return thatFunc.apply(
      this instanceof thatFunc?this :This,[...outherArgs,...innerArgs]
    )

  }
  // 考虑到不能污染到thatFunc的prototype，这里使用Object.create()
  fBind.prototype = Object.create(thatFunc.prototype)
  // 返回一个函数
  return fBind
}
```

```js
// 一个简单的例子
function fn(a, b) {
  console.log(this, a + b)
}
fn.mybind({
  a: 1
}, 1, 2)() 
//{a: 1} 3
```

> 参考文章：掘金文章：https://juejin.cn/post/6983934602196811789#heading-53

>参考文章：掘金文章：https://juejin.cn/post/6844903906279964686#heading-11

