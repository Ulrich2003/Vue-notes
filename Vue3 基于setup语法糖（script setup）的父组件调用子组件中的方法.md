# Vue3 基于setup语法糖（script setup）的父组件调用子组件中的方法🍬
前置知识：[Vue中让子组件给父组件传递数据的3中方法](https://blog.csdn.net/weixin_45525653/article/details/122906270?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165685489216781685330032%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fblog.%2522%257D&request_id=165685489216781685330032&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~blog~first_rank_ecpm_v1~rank_v31_ecpm-4-122906270-null-null.185%5Ev2%5Econtrol&utm_term=ref&spm=1018.2226.3001.4450)

⭕️ 知识点：vue3；setup语法糖；组件ref；
⭕️ 以下例子实现了在父组件中，点击按钮，调用子组件中的changeNum（）方法
父组件：

```html
<template>
  <Son1 ref="son1" />
  <button @click="changeNum">点击调用子组件中的方法</button>
</template>

<script setup>
import Son1 from "./components/Son1.vue";
import { ref } from "vue";
// 关键代码
let son1 = ref();
function changeNum(){
  son1.value.changeNum()
}
</script>
```
子组件：

```html
<template>
  <div>Son1: {{num}}</div>
</template>
<script setup>
import {ref,defineExpose} from 'vue'
let num = ref(10);
// eslint-disable-next-line no-unused-vars
function changeNum(){
  num.value = 100
}
// 记得暴露
defineExpose({
  changeNum
});
</script>
```

