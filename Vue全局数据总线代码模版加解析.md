# Vue全局数据总线代码模版加解析

### 前言
首先，全局总线并不难，理解起来也不算很乱，但需要有下面几个前置知识：
1. [🔗 Vue组件自定义事件](https://blog.csdn.net/weixin_45525653/article/details/122906270?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165268614916782246483133%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=165268614916782246483133&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-1-122906270-null-null.nonecase&utm_term=%E7%BB%84%E4%BB%B6%E9%97%B4&spm=1018.2226.3001.4450)
上面的链接，如果你有点基础可以看这篇文章回顾下，如果没有基础推荐你去找更好的文章
2. 知道自定义事件绑在谁身上，就去找谁触发
3. 如果你知道消息订阅与发布（PubSub），这篇文章会更好理解


### 正文
本文的代码模版实现了如下图所示的数据传递例子：
![在这里插入图片描述](https://img-blog.csdnimg.cn/b4d5ce799f6646a4aa86aa88175eefd3.png)
**说明：这个例子即使不使用全局数据总线，也是可以实现的。使用全局数据总线带来的优点是，有一个「工具人$bus」可以给我们做传播媒介，无论哪两个组件之间传递和接收数据都没有问题**

**核心思想是：在组件间传递数据之前，发起者要去找 `$bus` 注册一个自定义事件，接收者要去`$bus`触发发起者注册的事件（发起者将事件绑在`$bus`身上，所以接收者要去找`$bus`触发）** 

##### 1⃣️ 先要造一个工具人「$bus」

**在main.js 里面造一个`$bus`,也就是我们说的全局数据总线**
解析：框里的`this`指的是Vue实例对象。将Vue实例对象对象绑定到Vue原型的`$bus`上，这样脚手架中所有的.vue组件的this中，都能找到`$bus`了
![在这里插入图片描述](https://img-blog.csdnimg.cn/a2c3e8457629485c8554b3272bb38926.png)
2⃣️ 在`Brother1.vue`中为`$bus`绑定一个自定义事件，并传递要发送给其他组件的值
![在这里插入图片描述](https://img-blog.csdnimg.cn/b978a37b6e074836b039f6459bfc589f.png)

3⃣️ 在`Brother2.vue`中触发`$bus`中的`message`事件，拿到`Brother1.vue`传递出来的值
![在这里插入图片描述](https://img-blog.csdnimg.cn/55a8695935c64a7e9402802284a3b107.png)

### 实现效果：![在这里插入图片描述](https://img-blog.csdnimg.cn/1798ea713bd4495782fef6248d666562.png)
### 代码模板：
`main.js`
```javascript
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

new Vue({
  render: h => h(App),
  beforeCreate(){
    Vue.prototype.$bus = this
  }
}).$mount('#app')
```
`Brother1.vue`

```html
<template>
  <div>
    <button @click="sendMsg">点我传递一串Str给兄弟组件Brother2</button>
  </div>
</template>

<script>
export default {
  data(){
    return{
      str:"务必认识真理"
    }
  },
  methods:{
    sendMsg(){
      this.$bus.$emit('message', this.str)
    }
  },
}
</script>
```
`Brother2.vue`

```html
<template>
  <div></div>
</template>

<script>
export default {
  mounted(){
    this.$bus.$on('message',(data)=>{
      console.log('我是Brother2，收到了Brother1发来的信息：',data);
    })
  }
}
</script>
```

