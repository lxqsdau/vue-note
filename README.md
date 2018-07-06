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

