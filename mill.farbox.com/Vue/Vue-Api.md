---
date: 2017-5-11 09:48:40
status: public
title: Vue-API
---

### 全局配置
`Vue.config`是一个对象,包含Vue的全局配置.可以在应用启动之前修改下列属性:

---

#### slient
```js
//取消vue所有日志和警告
Vue.config.slient = true;
```

#### optionMergeStrategies
//todo 自定义合并策略

#### devtools
```js
//务必在加载Vue之后,立即同步设置以下内容
Vue.config.devtools = true;
```

配置是否允许`vue-devtools`检查代码.开发版默认为`true`,生产版本默认为`false`.

#### errorHandle
```js
Vue.config.errorHandle = function(err,vm){
  //handle error
}
```

指定组件的渲染和观察期间未捕获错误的处理函数.这个处理函数在被调用时,可获取错误的信息和Vue的实例.
//todo

### 全局API

---

#### Vue.extend({object}options)
