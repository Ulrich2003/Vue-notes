# Vue3中的ref函数
### 前言

vue2中我们只要是写在data中的数据就能成为一个响应式的数据，但为什么vue3定义响应式数据要这么难呢❓

- [Vue3中为什么要用ref和reactive定义数据？](https://blog.csdn.net/rgmyrg/article/details/123001140)
- Vue3.0 把创建响应式对象从组件实例初始化中抽离了出来，通过暴露 API 的方式将响应式对象创建的权利交给开发者，开发者可以自由的决定何时何地创建响应式对象

<hr>

### 什么是 ref() 

ref函数的作用：创建一个包含响应式数据的引用对象（reference obj）

```html
<script>
import {ref} from 'vue'
export default {
  name: 'Person',
  setup(){
    // 基本类型
    let name = ref('Ulrich')
    // 对象类型
    let job = ref({jobName : 'front-end engineer'})
    return {
      name,
      job
    }
  }
}
</script>
```
1⃣️ `ref()`函数接收的数据可以是基本类型，也可以是对象类型

2⃣️ 基本类型的数据，响应式依旧靠`Object.defineProperty()` 的`get`和`set`完成的

3⃣️ 对象类型的数据：内部实现是依靠`reactive`函数


### 如何在`<template></template>`中读取响应式数据？

```html
<template>
  <h3>{{name}}</h3>
  <h3>{{job.jobName}}</h3>
</template>
```

**output / 输出结果：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/63598b5ade784af4b517948a8e5e022f.png)
### 如何在JS中操作ref函数包裹的响应式数据
需要通过`xxx.value`的形式来修改响应式数据：
```javascript
let change = function(){
	 // 修改基本类型的响应式数据
     name.value = 'Vichien'
     // 修改对象类型的响应式数据
     job.value.jobName = 'back-end engineer'
}
```








