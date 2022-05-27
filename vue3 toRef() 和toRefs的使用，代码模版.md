# vue3 toRef() 和toRefs的使用，代码模版

### toRef（）代码模版

```html
<template>
  <h3>{{ name }}</h3>
  <h3>{{ age }}</h3>
  <h3>{{ jobType }}</h3>
  <button @click="changePerson">修改person中的值</button>
</template>

<script>
import { reactive,toRef } from "@vue/reactivity";
export default {
  setup() {
    let person = reactive({
      name: "Ulrich",
      age: 22,
      job: {
        type: "front-end engineer",
      },
    });
    function changePerson(){
      person.name = 'Vichien'
      person.age = 18
    }
    return {
      // 如果写name:person.name，或是name:ref(person.name)的话，
      //修改person里面数据时，页面是不会不会依照person数据做响应式变化的
      name:toRef(person,'name'),
      age:toRef(person,'age'),
      jobType: toRef(person.job, "type"),
      changePerson
    };
  },
};
</script>
```

### toRefs（）代码模版

```html
<template>
  <h3>{{ name }}</h3>
  <h3>{{ age }}</h3>
  <h3>{{ job.type }}</h3>
  <button @click="changePerson">修改person中的值</button>
</template>

<script>
import { reactive, toRefs } from "@vue/reactivity";
export default {
  setup() {
    let person = reactive({
      name: "Ulrich",
      age: 22,
      job: {
        type: "front-end engineer",
      },
    });
    function changePerson() {
      person.name = "Vichien";
      person.age = 18;
    }
    return {
      ...toRefs(person),
      changePerson,
    };
  },
};
</script>
```

