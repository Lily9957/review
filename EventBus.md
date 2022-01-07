**EventBus**

EventBus:又称为事件总线。在Vue中可以使用 EventBus 来作为沟通桥梁的概念，就像是所有组件共用相同的事件中心，可以向该中心注册发送事件或接收事件，所以组件都可以上下平行地通知其他组件。

**使用场景**

在做vue项目时，偶遇到需要兄弟组件通信，但是你又不想用Vuex做一个全局状态管理，觉得有点大材小用了。这时候，就可以使用EventBus，快捷方便的解决这个问题。



**如何使用EventBus**

在Vue项目中如何使用EventBus来实现兄弟组件之间的通信呢？具体可分为以下几个步骤。



**1、初始化**

首先我们需要创建时间总线并将其导出，以便其他模块可以使用或者监听它。创建utils文件夹，在其内部创建一个event-bus.js文件

```js
//utils/event-bus.js
import Vue from 'vue'
export const EventBus = new Vue();
```



**2、发送事件**

创建好EventBus后，我们就可以使用了。在使用之前要将EventBus引入到组件中。

```js
import { EventBus } from "../utils/EventBus";
```

现在假若我们需要通信的组件分别是A、B，A要告诉B，“Hello，我是A”；让我们开始给B发送信息吧。

```js
//component A
msg = "Hello，我是A"
//绑定了一个点击事件去发送信息
handleClick(): void {
  EventBus.$emit("msg", this.msg);
}
```



**3、接收事件**

A已经给B发送信息了，那B该怎么接收呢？

第一步，引入：

```js
import { EventBus } from "../utils/EventBus";
```

第二步，接收：

```js
  msg = "";
  mounted() {
    EventBus.$on("msg", (msg: string) => {
      console.log(msg, "**");
      this.msg = msg;
    });
  }
```



**4、移除事件**

```js
  beforeDestroy() {
    EventBus.$off('msg')
  }
```

