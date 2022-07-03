# Vue3 script setup语法糖中使用v-model对子组件进行双向数据绑定🍬

**参考文章：**[vue3 v-model变化](https://blog.csdn.net/yusirxiaer/article/details/122744772)

v-model对子组件进行双向数据绑定的意义：
在某些情况下，**我们可能需要对某一个 prop 进行“双向绑定”**，vue3提供的`v-model`可以很好的实现这个需求。

父组件：

```html
<template>
  <Son v-model:count="count"></Son>
</template>

<script setup>
import Son from "./components/Son.vue";
import { ref } from "vue";

let count = ref(100);
</script>
```
子组件：

```html
<template>
    <div >
        {{count}}
    </div>
    <button @click="emit('update:count',count+1)">加1</button>
</template>

<script setup>
import { defineProps,defineEmits } from 'vue';
// eslint-disable-next-line no-unused-vars
const props = defineProps(['count'])
const emit = defineEmits(['update:count'])
</script>
```


