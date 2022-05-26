# Vue3 reactive()的使用。reactive()对比ref()的优点

作用：定义一个**对象类型**的响应式数据，基本类型用不了reactive()

语法：`const 代理对象 = reactive(源对象)` 

- 接收一个对象或数组
- 返回一个代理对象（proxy对象）

reactive定义响应式数据是深层次的，对象中的对象，数组中的数组都能被监视到状态的修改（或叫值的修改）
reactive内部是基于ES6的Proxy实现的，通过代理对象操作源对象内部数据进行操作。

### reactive()在vue3中的使用

```html
<script>
import {reactive} from 'vue'
export default {
  name: 'Person',
  setup(){
    
    let person = reactive({
      name:'ulrich',
      age:22,
      job:{
        type:'front-end engineer',
        salary:'30k',
      },
      hobby:['学习','骑行','写博客']
    })
	
	// 修改person中的数据
    let change = function(){
      person.name = 'vichien'
      person.job.type = 'back-end engineer'
      person.hobby[2] = '和产品经理对线'
    }

    return {
      person,
      change
    }
  }
}
</script>
```

### 在`<template></template>`模板中如何使用reactive()包裹的响应式数据❓

```html
<template>
  <h3>{{person.name}}</h3>
  <h3>{{person.age}}</h3>
  <h3>{{person.job.type}}</h3>
  <h3>{{person.job.salary}}</h3>
  <h3>{{person.hobby}}</h3>
  <button @click="change">点我修改数据</button>
</template>
```

### output / 输出效果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/3d0caa6becdc4468b439d0c20ca8f914.png)

<hr>

### ⭕️ reactive对比ref

1⃣️ 从定义数据角度对比：
 
 - ref用来定义：基本类型数据
 - reactive用来定义：对象或数组类型数据
 - 备注：ref也可以用来定义对象（或数组）类型数据，它内部会自动通过 `reactive` 转为代理对象。 
 - ⚠️ 基本数据类型同样可以包裹在对象中，再放到ref里面形成响应式数据

2⃣️ 从原理角度对比

- ref通过`Object.defineProperty`的`get()`和`set()`来实现响应式（数据劫持）
- reactive通过`proxy`来实现响应式，并通过`Reflect`来操作源对象内部的数据

3⃣️ 从使用角度对比

- ref定义的数据：操作数据需要`.value`，读取数据时模板中直接读取不需要`.value`

- reactive定义的数据：操作数据与读取数据均不需要`.value`

### 进一步学习

[Vue2、Vue3响应式实现方案原理模拟，只是简单的模拟](https://blog.csdn.net/weixin_45525653/article/details/124985305?spm=1001.2014.3001.5501)


