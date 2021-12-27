---
title: defineProperty和Proxy
date: 2021-12-27 16:40:20
tags:
---


- **Object.defineProperty()**
直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。
```javascript
  var object1 = {}
  Object.defineProperty(object1, name, {
    value: 'nyw',
    writable: false
  })
```
第三个字段描述:分为数据描述符和存取描述符
**数据描述符:**
- configurable:false
当且仅当该属性的 configurable 键值为 true 时，该属性的描述符才能够被改变，同时该属性也能从对应的对象上被删除。
默认为 false。
. 属性第一次设置后是否可以被修改
. 属性是否可以被删除
在非严格模式下，属性配置configurable:false后进行删除操作会发现属性仍然存在。
而在严格模式下会抛出错误。
- enumerable:false
当且仅当该属性的 enumerable 键值为 true 时，该属性才会出现在对象的枚举属性中（for in或者Object.keys()）。
默认为 false。
数据描述符还具有以下可选键值：

- value:undefined
该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）。
默认为 undefined。
- writable:false
当且仅当该属性的 writable 键值为 true 时，属性的值，也就是上面的 value，才能被赋值运算符 (en-US)改变。
默认为 false。

**存取描述符:**
- get 、set
defineProperty实现对象属性的监听(数据劫持)。vue2原理~~
```javascript
var user = {};

var initName = ''
Object.defineProperty(user, "name", {
    get: function(){
        console.log('get name')
        return initName
    },
    set: function(val){
        console.log('set name')
        initName = val
    }
});
// get name
console.log(user.name)
// set name
user.name = 'new'
```
**如果一个描述符同时拥有 value 或 writable 和 get 或 set 键，则会产生一个异常。**
