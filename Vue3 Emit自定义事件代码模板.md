App.vue 中
```html
<template>
  <Emit @myEmit="showMessage"></Emit>
</template>

<script>
import Emit from './components/Emit.vue'
export default {
  name: "App",
  components: {Emit},
  setup() {
    function showMessage(msg){
      alert(msg)
    }
    return {showMessage};
  },
};
</script>
```
Emit 组件中
```html
<template>
  <div @click="$emit('myEmit','这是一条触发Emit组件后传递的消息')">绑定自定义事件的组件</div>
</template>
<script>

export default {
  emits:['myEmit'],
  setup() {
    return {
      
    };
  },
};
</script>
```

