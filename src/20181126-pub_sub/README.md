## 手摸手带你实现一个EventEmitter

![event-bus](./assets/event-bus.png)


在日常工作跨模块开发时，很常见的一个场景：不同模块间的事件通信。

以下给出ES5、ES6两种实现方式。

### ES5实现

```js
var events = {}
var Events = {
  on: function (key, fn) {
    if (typeof fn !== 'function') {
      return
    }
    events[key] = events[key] || []
    events[key].push(fn)
  },
  once: function (key, fn) {
    if (typeof fn !== 'function' || (fn.once && fn.hasExeced)) {
      return
    }
    fn.once = true
    fn.hasExeced = false
    events[key] = events[key] || []
    events[key].push(fn)
  },
  trigger: function (key) {
    var args = [].slice.call(arguments, 1)
    var fnList = events[key] || []
    fnList.forEach(function (item) {
      if (typeof item === 'function') {
        if (item.once && item.hasExeced) {
          return
        } else if (item.once && !item.hasExeced) {
          item.hasExeced = true
          item.apply(window, args)
        } else {
          item.apply(window, args)
        }
      }
    })
  }
}
```
使用
```js

```

### ES6实现

#### 订阅者

```js

```

#### 观察者

```js

```

#### 应用

```js

```

### 终极版

完整代码见[@careteen/event-emitter](https://github.com/careteenL/eventEmitter)

### 总结
