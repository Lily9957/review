### Vue.nextTick()的原理

vue是异步执行DOM更新鹅，一旦观察到数据的变化，vue会开启一个异步队列(不会立刻执行)，把同一个event loop中观察数据变化的watcher推送进这个队列中。



在下一次事件循环时，vue会清空当前的异步队列，进行dom更新



vm.data = "new value",dom不会马上更新，而是在异步队列被清除时，下一个异步队列开启时，才会更新DOM



事件循环的顺序：

宏任务---->微任务----->  UI render

宏任务：promise.then、MutationObserve

微任务：setImmediate、setTimeout



一般什么时候用到nextTick？

1】在数据变化后要执行某个操作，而这个操作依赖因你数据改变而改变的DOM，这个操作就应该被放到nextTick回调中

```js
<template>
  <div v-if="loaded" ref="test"></div>
</template>

async showDiv(){
  this.loaded = true
  this.$refs.test....//同步获取不到test，因为DOM立即没有更新
  
  await Vue.nextTick();
  this.$refs.test....//这里就可以拿到了
}
```

