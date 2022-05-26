# Vue3中setup()函数收到的两个比较重要的值
setup()函数能接收到两个形参，一个是`props`，另外一个是`context`。props即父组件传递给子组件的参数，context意思是上下文，里面有一个`emit('事件名', 事件回调函数收到的值)`函数比较常用，可替代vue2绑定在vm身上的`this.$emit('事件名', 事件回调函数收到的值);`

子组件：

```html
<template>
  <h3>{{person.name}}</h3>
  <h3>{{person.age}}</h3>
  <button @click="sayHello">点我触发Person身上的hello事件</button>
</template>

<script>
import {reactive} from 'vue'
export default {
  name: 'Person',
  // 接收到的参数
  props:['name','age'],
  // 声明自定义事件
  emits:['hello'],
  setup(props,context){
    let person = reactive({
      name:props.name,
      age:props.age,
    })

    function sayHello(){
      // 触发自定义事件
      context.emit('hello','你好')
    }

    return {
      person,
      sayHello
    }
  }
}
</script>
```
父组件：

```html
<template>
  <Person name="Ulrich" age="22" @hello="showHelloMsg"></Person>
</template>

<script>
import Person from "./components/Person.vue";
export default {
  name: "App",
  components: {
    Person,
  },
  setup() {
    function showHelloMsg(value) {
      console.log("hello事件被触发，收到的参数是: " + value);
    }

    return {
      showHelloMsg
    };
  },
};
</script>
```

