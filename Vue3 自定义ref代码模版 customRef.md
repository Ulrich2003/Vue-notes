# Vue3 自定义ref代码模版 customRef

```html
<template>
  <input type="text" v-model="keyWord">
  <h3>{{keyWord}}</h3>
</template>

<script>
import { customRef } from "vue";
export default {
  setup() {
    let keyWord = myRef('hello')

    function myRef(value){
      return customRef((track,trigger)=>{
        return {
          get(){
            track() // 通知vue追踪value的变化
            return value
          },
          set(newValue){ // newValue 是input修改后的值
            value = newValue
            // 通知vue去重新解析模板
            trigger()
          }
        }
      })
    }

    return {
      keyWord 
    };
  },
};
</script>
```

