# vue-note


## 1、注册组件，使用驼峰命名法
渲染使用-

```js
import { XHeader, XTable, PopupPicker } from 'vux';
components: {
    XHeader,
    XTable,
    PopupPicker
},
<x-header></x-header>
```

##  2、绑定点击事件
```js
<div @click="greet"></div>

methods: {
   greet() {} 
}
```

## 3、vue 项目启动时将localhost替换成制定的ip地址
> * node启动vue项目时地址一般都是http://localhost:8080
> * config->index.js 中的host：‘localhost’换成host：‘你的本机ip’就可以了
```js
module.exports = {
  dev: {
    host: '192.168.1.100'
  }
}
```
## 4、this.$nextTick(function(){})

> * Vue 实现响应式并不是数据发生变化之后 DOM 立即变化，而是按一定的策略进行 DOM 的更新
> * $nextTick 是在下次 DOM 更新循环结束之后执行延迟回调，在修改数据之后使用 $nextTick，则可以在回调中获取更新后的 DOM
> * 如果一个函数中，既有主题的data变化，也有ajax后的data变化，外部的nextTick会先执行，ajax后的data变化会触发ajax里的nextTick执行

```jsx
<div class="app">
    <div ref="msgDiv">{{msg}}</div>
    <div v-if="msg1">Message got outside $nextTick: {{msg1}}</div>
    <div v-if="msg2">Message got inside $nextTick: {{msg2}}</div>
    <div v-if="msg3">Message got outside $nextTick: {{msg3}}</div>
    <button @click="changeMsg">
        Change the Message
    </button>
</div>

new Vue({
  el: '.app',
  data: {
    msg: 'Hello Vue.',
    msg1: '',
    msg2: '',
    msg3: ''
  },
  methods: {
    changeMsg() {
      this.msg = "Hello world."
      this.msg1 = this.$refs.msgDiv.innerHTML
      this.$nextTick(() => {
        this.msg2 = this.$refs.msgDiv.innerHTML
      })
      this.msg3 = this.$refs.msgDiv.innerHTML
    }
  }
})

```
> 输出
> * Message got outside $nextTick: Hello Vue.
> * Message got inside $nextTick: Hello world.
> * Message got outside $nextTick: Hello Vue.

## 父子组件通信
* 父 -> 子
> 父组件是通过props属性给子组件

* 子 -> 父
> vue2.0只允许单向数据传递，通过触发事件来改变组件的数据
子组件
```js
<template>
    <div @click="open"></div>
</template>

methods: {
   open() {
        this.$emit('showbox','the msg'); // 触发showbox方法，'the msg'为向父组件传递的数据
    }
}
```
父组件

```js
<child @showbox="toshow" :msg="msg"></child> //监听子组件触发的showbox事件,然后调用toshow方法

methods: {
    toshow(msg) {
        this.msg = msg;
    }
}
```

## vue不能检测一下data变动情况
> * obj新增的属性，vue是监听不到的  --> this.$set(this.obj, 'sex', 'sex'); 只有当实例被创建时data中存在的属性才是响应式的
> * 利用索引直接设置一项 this.attr[0] = 3 ---> 解决方法 vm.items.splice(indexOfItem, 1, newValue)  或 Vue.set(vm.items, indexOfItem, newValue)
> * 直接设置数组的length
> * filter(), concat() 和 slice()不会改变原数组，但会返回一个新数组，可以用新数组替换旧数组


## v-for v-if
> * 当它们处于同一节点，v-for 的优先级比 v-if 更高，这意味着 v-if 将分别重复运行于每个 v-for 循环中。当你想为仅有的一些项渲染节点时，这种优先级的机制会十分有用
```js
<li v-for="todo in todos" v-if="!todo.isComplete">
  {{ todo }}
</li>
// 上面的代码只传递了未完成的 todos。
```

## 简写
> * v-bind:class --> :class
> * v-on:click --> @click




















