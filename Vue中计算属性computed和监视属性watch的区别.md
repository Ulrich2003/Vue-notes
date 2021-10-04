# Vue中计算属性computed和监视属性watch的区别

### computed和watch之间的区别
- computed能完成的功能，watch都能完成
- watch能完成的功能，computed不一定能完成，例如watch可以进行异步操作
### 使用中的原则
- 所被Vue管理的函数，最好写成普通函数，这样this的指向才是vm或组件实力对象
- 所有不被Vue所管理的函数（定时器⏲️的回调函数，ajax的回调函数，Promise的回调函数），最好写成箭头函数，这样this的指向才是vm或组件实例对象
