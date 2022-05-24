# vuex3配置，vuex3代码模板，适配vue2版本
### 前言：
1. 本文章不适合 `vue 3` 版本，只适合 `vue2` 版本
2. `vuex3` 适配 `vue2`， `vuex4` 适配 `vue3`
3. vuex3 原理图
![在这里插入图片描述](https://img-blog.csdnimg.cn/fd5310bf8e704904915d78ed4aa45bff.png)
原理图展示的是组件修改存放在vuex中的值，首先先将要（修改的数据名以及修改的数据值）传递到`actions对象的`方法中`actions对象的方法`里面可以与后端api连接，也可以处理从组件拿到的value值（数据）做一些数据判断的逻辑，再将这个value值提交到mutations对象里对应的方法里面。
`mutations对象`直接对接vuex开发者工具，这里修改的数据能被开发者工具监视到。在`mutations对象`的方法中，对存放在state对象里面的值直接进行修改，修改的结果会被重新渲染到组件中，这个过程就是「组件修改存放在vuex中的值」的过程。
值得注意的是，组件也是可以绕过actions对象直接和mutations对象中的方法对话的

### 安装

```
npm i vuex@3
```

### 配置Vuex的Store
1⃣️ `main.js`
以下为代码模版
```javascript
import Vue from 'vue'
import App from './App.vue'
import Vuex from 'vuex'
import store from './store'

Vue.use(Vuex)

new Vue({
  store,
  render: h => h(App)
}).$mount('#app')
```
2⃣️ 在`src`目录下创建一个目录`store`
![在这里插入图片描述](https://img-blog.csdnimg.cn/954cdf5e744e4f248865b7b70e3b6c9e.png)
3⃣️ 在store文件夹 📁 里面创建`index.js`，并参加一个自定义名字的js文件（图里用`calculatorOptions.js`）为例子，该文件用来封装vuex操作中的几个重要的对象。
![在这里插入图片描述](https://img-blog.csdnimg.cn/fc0741bb72234014926814c9fefac87a.png)`calculatorOptions（自定义文件名）.js`
以下为代码模版，里面存在的一些方法目的是为了说明功能，直接复制该代码放到文件里，再对代码无关部分进行删除重写即可。

```javascript
// 该文件用于创建vuex中最为核心的store
export default {
    // 开启命名空间，让组件只能通过对应的命名空间访问到对象中的方法
    namespaced:true,
    // 用于响应组件中的动作
    actions: {
        add(context, value) {
            // ....此处省去一堆代码（actions里可对拿到的value值进行处理）
            console.log("actions中的add()被调用了", context, value);
            // 将value交给mutations对象中的ADD()处理
            context.commit("ADD", value);
        },
        decrement(context, value) {
            // ....此处省去一堆代码（actions里可对拿到的value值进行处理）
            // 将value交给mutations对象中的DECREMENT()处理
            context.commit("DECREMENT", value);
        },
    },

    // 用于操作数据
    mutations: {
        ADD(state, value) {
        	// 操作state，修改vuex中state的数据
            state.sum += value;
        },
        DECREMENT(state, value) {
        	// 操作state，修改vuex中state的数据
            state.sum -= value;
        },
    },

    // 用于将state中的数据进行加工（不是必要的）
    getters: {
    	// 该方法用于返回state中sum值放大10倍后的值
        bigSum(state) {
            return state.sum * 10;
        },
    },

    // 用于存储数据
    state: {
            sum: 0,
    },
};
```

`index.js`
以下为代码模版，里面存在的一些方法目的是为了说明功能，直接复制该代码放到文件里，再对代码无关部分进行删除重写即可。

```javascript
import Vue from "vue";
import Vuex from "vuex";
// 引入js文件
import CalculatorOptions from './calculatorOptions'
Vue.use(Vuex);

// 创建并暴露stroe
export default new Vuex.Store({
    modules:{
        CalculatorOptions
    }
});
```
### 组件中使用Vuex
⭕️ 组件中经常会用到的几个操作vuex的方法：
```javascript
<template>
    <div>
        <button @click="add(1)">为sum加1</button>
        <button @click="DECREMENT(1)">为sum减1</button>
    </div>
</template>

<script>
import {mapMutations,mapActions} from 'vuex'

export default {
    name: 'Calculator2',
    methods: {
	   // 二选一
        ...mapMutations('CalculatorOptions',{add:'add'}),
        ...mapMutations('CalculatorOptions',['add']),
       // 二选一
        ...mapActions('CalculatorOptions',{add:'add'}),
        ...mapActions('CalculatorOptions',['add'])
	},
};
</script>
```

1⃣️ 操作actions

- ⭕️ 对象形式写法：`...mapActions('命名空间',{该组件内可调用的方法名:'actions对象里面对应的方法名'})`
- 🌰 例子：`...mapActions('CalculatorOptions',{add:'add'})`
- ⭕️ 数组形式写法：`...mapActions('命名空间',['方法名'])`，要求该组件内可调用的方法名和actions对象里面对应的方法名要一致才可以这么写
- 🌰 例子：`...mapActions('CalculatorOptions',['add'])`


2⃣️ 操作mutations

- ⭕️ 对象形式写法：`...mapMutations('命名空间',{该组件内可调用的方法名:'mutations对象里面对应的方法名'})`
- 🌰 例子：`...mapMutations('CalculatorOptions',{add:'ADD'})`
- ⭕️ 数组形式写法：`...mapMutations('命名空间',['方法名'])`，要求该组件内可调用的方法名和mutations对象里面对应的方法名要一致才可以这么写
- 🌰 例子：`...mapMutations('CalculatorOptions',['DECREMENT'])`

3⃣️ 读取vuex中state中的数据，以及读取vuex中getters对象中的方法返回的数据
一下内容和1⃣️ 2⃣️ 写法类似，不过多阐述

```javascript
<template>
    <div>
        <h1>sum:{{sum}}</h1>
        <h1>放大10倍后的sum:{{bigSum}}</h1>
    </div>
</template>

<script>
	// 引入vuex内置封装的方法
	import {mapState,mapGetters} from 'vuex'

	export default {
    	name: 'Calculator',
    	computed:{
        	/* 借助mapState生成计算属性，从state中读取数据。 */
        	// 对象写法
        	...mapState('CalculatorOptions',{sum:'sum'}),
        	// 数组写法
        	...mapState('CalculatorOptions',['sum']),

        	/* 借助mapGetters生成计算属性，从getters中读取数据。 */
        	// 对象写法
        	...mapGetters('CalculatorOptions',{bigSum:'bigSum'}),
        	// 数组写法
        	...mapGetters('CalculatorOptions',['bigSum'])
    	}
	};
</script>
```

