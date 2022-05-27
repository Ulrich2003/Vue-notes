# Vue3 计算属性computed()和监视watch的使用，代码模板

### computed()

```html
<script>
import {reactive,computed} from 'vue'
export default {
  name: 'Person',
  setup(){
    let person = reactive({
      name:'Ulrich',
      age:22,
    })

    // 计算属性 - 简写 - 回调函数的形式
    person.nameLength = computed(()=>{
        return person.name.length
    })

    // 计算属性 - 完整写法 - 对象的形式
    person.nameLength = computed({
      get(){
        return person.name.length
      },
      // 只有这样写，计算属性的值才可以被用户直接修改，不然控制台会报错
      set(value){
        person.name += value
      }
    })

    return {
      person
    }
  }
}
</script>
```

### watch()

⚠️ 🕳️🏃🕳️  **两个巨坑：**

- 监视reactive定义的响应式数据时：oldValue无法正确获取，没办法通过`deep:false`关闭深度监视
- 监视reactive定义的响应式数据中的某个属性时：oldValue无法正确获取，deep配置有效

```html
<script>
import { reactive, ref, watch } from "vue";
export default {
  name: "Person",
  setup() {
	......
    // 只监视一个响应式数据
    watch(num1,(newValue, oldValue) => {
        console.log(
          `num1的值被改变了，num1的新值是:${newValue},num1的旧值是:${oldValue}`
        );
      },{ immediate: true });

    // 监视多组响应式数据
    watch([num1, num2],(newValue, oldValue) => {
        console.log(`监视的值被改变了，新值是:${newValue},旧值是:${oldValue}`);
      },{ immediate: true });

    // 监视reactive所定义的一个响应式数据
    // ⚠️ 注意：此处无法正确获得oldValue，并且无解，框架问题
    // (即使想用ref包裹对象，底层原理也是reactive)
    // ⚠️ 注意：这里即使配置`deep:false`，也无法关闭深度监视
    watch(person,(newValue, oldValue) => {
        console.log(`监视的值被改变了，名字的新值是:${newValue.name},旧值是:${oldValue.name}`);
      }
    );

    // 监视reactive所定义的一个响应式数据中的某个属性
    // 第一个参数不能直接写person.age,要写成一个回调函数的形式
    // 可以正确获得oldValue
    watch(()=>person.age,(newValue,oldValue)=>{
      console.log(`person的age被修改了，年龄的新值是${newValue},旧值是:${oldValue}`);
    })

    // 监视reactive所定义的一个响应式数据中的某些属性
    watch([()=>person.name,()=>person.age],(newValue,oldValue)=>{
      console.log(`person的一些属性被修改了，新值是${newValue},旧值是:${oldValue}`);
    })

    // 特殊情况 (这里必须开启deep，不然没法深度监视)
    watch(()=>person.job,(newValue,oldValue)=>{
      console.log(`person的job变化了，新值是${newValue.s1.salary},旧值是:${oldValue.s1.salary}`);
    },{deep:true})

    return {
      ......
    };
  },
};
</script>
```

### watchEffect()
特点：不用指明监视了哪个属性，监视的回调用用到了哪个属性，就监视哪个属性

⭕️ `watchEffect`有点像`computed`

- 但computed更注重的是计算出来的值，所以必须写返回值
- 而watchEffect更注重过程，所以不用写返回值 

```javascript
    // watchEffect里面用到了谁就监视谁
    watchEffect(()=>{
      person.name;
      person.age;
      console.log('watchEffect的回调被执行了');
    })
```

