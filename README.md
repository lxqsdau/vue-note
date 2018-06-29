# vue-note
vue笔记
Vue 使用

* 1、注册组件，使用驼峰命名法
渲染使用-

```
import { XHeader, XTable, PopupPicker } from 'vux';
components: {
    XHeader,
    XTable,
    PopupPicker
},
<x-header></x-header>
```

* 2、绑定点击事件
```
<div @click="greet"></div>

methods: {
   greet() {} 
}
```

* 3、vue 项目启动时将localhost替换成制定的ip地址
> node启动vue项目时地址一般都是http://localhost:8080
> config->index.js 中的host：‘localhost’换成host：‘你的本机ip’就可以了
```
module.exports = {
  dev: {
    host: '192.168.1.100'
  }
}
```
