---
title: "学习 Object.defineProperty"
date: 2019-02-23
permalink: "/javascript/学习Object.defineProperty"
meta:
  - name: description
    content: 一个热爱文学的伪程序猿，张努力，Node，webpack，JavaScript，爱好者，博客
  - name: keywords
    content: 一个热爱文学的伪程序猿，张努力，Node，webpack，JavaScript，爱好者，博客
---

# 学习 Object.defineProperty

## Object.defineProperty()

- 语法：

```javascript
Object.defineProperty(obj, prop, descriptor)

```

- 参数说明：

```json
 obj：(必需),目标对象
 prop：(必需),需定义或修改的属性的名字
 descriptor：(必需),目标属性所拥有的特性

```

### 针对属性，我们可以给这个属性设置一些特性，比如是否只读不可以写；是否可以被 for..in 或 Object.keys()遍历。

### 定义数据

```javascript

let obj = {
    a:'zhangnuli'
}

Object.defineProperty(obj,"zhangnuli",{
    configurable : true,
    enumerable : true,
    writable : true,
    value : "zhangnuli"
})

```

### 属性

- `configurable`：当且仅当该属性的 configurable 为 true 时，该属性描述符才能够被改变，同时该属性也能从对应的对象上被删除。默认为 false。
- `enumerable`：当且仅当该属性的 enumerable 为 true 时，该属性才能够出现在对象的枚举属性中。默认为 false。
- `writable`：当且仅当该属性的 writable 为 true 时，value 才能被赋值运算符改变。默认为 false。
- `value`：该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）。默认为 undefined。

### get 和 set

```javascript

let obj;

Object.defineProperty(obj,"a",{
     get:function(){
        return obj
    },
    set:function(val){
        obj=val;
    },
})

```

- 当我们获取值得时候会触发 get 方法,我们设置值的时候会触发 set 方法

- get 或 set 不是必须成对出现，任写其一就可以。如果不设置方法，则 get 和 set 的默认值为 undefined
