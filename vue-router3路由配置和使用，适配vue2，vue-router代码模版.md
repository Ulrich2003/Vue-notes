# vue-router3路由配置和使用，适配vue2，vue-router代码模版。只需要这篇文章就够了。
### 前言
- 本文只适合vue2，不适合vue3，vue3对应的路由版本是vue-router@4
- 文章可能有点长，内容有点多，可以通过窗口左下角的目录自取需要的内容阅读

![](https://img-blog.csdnimg.cn/865249154b2a49d6b2138fa78d40848b.png)


<hr>

### 安装 vue-router3

```
npm i vue-router@3
```
### 基本配置
1⃣️ 在src目录下新建一个router文件夹，在文件夹里面创建一个`index.js`文件
![在这里插入图片描述](https://img-blog.csdnimg.cn/261b74e2aa9e4c588d876f1f07455921.png)

2⃣️ 在`main.js`添加以下代码

```javascript
import Vue from 'vue'
import App from './App.vue'
import VueRouter from 'vue-router'
import router from './router'

Vue.use(VueRouter)

new Vue({
  el:'#app',
  render: h => h(App),
  router
}).$mount('#app')

```
3⃣️ 在`router`文件夹下的`index.js`中就可以编写路由规则啦

代码模版：

```javascript
import VueRouter from "vue-router";
import Home from '../pages/Home.vue'
import News from '../pages/News.vue'

// 创建并暴露一个路由器
export default new VueRouter({
    routes:[
        {
            path:'/自定义路由路径',
            component:路由路径对应的组件
        },
        {
            path:'/home',
            component:Home,
            // 二级路由编写
            children:[
                {   
                	// name 有点像路径别名，在多级路由下很有优势
        			// 表现在不用写一长串从父到子的路由地址
        			// 注意：写了name后依旧得写path
        			name:'news',
                    // 二级路由的path不需要带 '/'
                    path:'news',
                    component:News
                }
            ]
        }
    ]
})
```
### 如何使用路由做跳转？

1⃣️ 在页面中书写以下代码能实现路由跳转：

```html
<router-link to="/home">点击跳转到Home组件</router-link>
<!-- 指定路由对应的组件渲染的位置 -->
<router-view />
```
2⃣️ 如何跳转二级路由❓

```html
<router-link to="/home/news">NEWS</router-link>
```
3⃣️ 跳转路由时如何携带参数❓

#### 利用query携带参数

字符串写法：

```html
要跳转路由的地方：
<!-- 字符串写法（这里利用的是path来跳转） -->
<router-link to="/home/news?newsId=001&newsContent=这是一条新闻">NEWS</router-link>

路由对应的组件里：
<template>
  <div>
    <h2>NEWS组件</h2>    
    新闻编号：{{ $route.query.newsId }}
    新闻编号：{{ $route.query.newsContent }}
  </div>
</template>
```

对象写法：
```html
要跳转路由的地方：
 <!-- 对象写法（这里利用的是name来跳转） -->
      <router-link :to="{
          name:'news',
          query:{
            newsId:'002',
            newsContent:'这是一条新闻'
          }
      }">跳转到News组件</router-link>

路由对应的组件里：
<template>
  <div>
    <h2>NEWS组件</h2>    
    新闻编号：{{ $route.query.newsId }}
    新闻编号：{{ $route.query.newsContent }}
  </div>
</template>
```

#### 利用params携带参数
在`router`文件夹下的`index.js`中需要使用占位符声明接收params参数

```javascript
import ......

export default new VueRouter({
    routes:[
        ......
        {
            path:'/home',
            component:Home,
            children:[
                {   
                    name:'news',
                    // 使用占位符声明接收params参数
                    path:'news/:id/:content',
                    component:News
                }
            ]
        }
    ]
})
```
字符串写法：

```html
要跳转路由的地方：
<!-- 字符串写法（这里利用的是path来跳转） -->
<router-link to="/home/news/003/这是一条新闻">点击跳转到News组件</router-link>


路由对应的组件里：
<template>
  <div>
    <h2>NEWS组件</h2>    
    新闻编号：{{ $route.params.id }}
    新闻编号：{{ $route.params.content }}
  </div>
</template>
```
对象写法：
```html
要跳转路由的地方：
 <router-link :to="{
          name:'news', // 这里只能用name，不能用path
          params:{
            id:'002',
            content:'这是一条新闻'
          }
      }">跳转到News组件</router-link>

路由对应的组件里：
<template>
  <div>
    <h2>NEWS组件</h2>    
    新闻编号：{{ $route.params.id }}
    新闻编号：{{ $route.params.content }}
  </div>
</template>
```


### 进一步学习
[vue路由router的props配置](https://blog.csdn.net/weixin_45525653/article/details/124951457?spm=1001.2014.3001.5501)


### router-link 的replace属性

```html
<router-link to="..." replace >...</router-link>
```
加上replace最直观的感受是跳转完组件后，没办法通过浏览器返回按钮直接返回到跳转前的组件了。🔙


### 编程式路由导航
没说的那么高大上，简言之就是把路由标签搬到js代码里而已。

```html
<template>
  <div>
    <button @click="toNewsPage">跳转到News组件</button>
    <!--路由组件展示的位置-->
    <router-view></router-view>
  </div>
</template>

<script>
export default {
  name: "Home",
  methods: {
    toNewsPage() {
      this.$router.push({
        name: "news", // 这里只能用name，不能用path
        params: {
          id: "002",
          content: "这是一条新闻",
        },
      });
    },
  },
};
</script>
```

### 缓存路由组件（保活路由组件）
作用：一般来说，不展示的路由组件会被立刻销毁。缓存路由组件就是为了让不展示的路由组件保持挂载，不被销毁，以待重写展示组件的时候，填写在组件中的信息能够恢复。

⚠️ 注意：`include=""`里面填写的是要缓存的**组件的名称**❗️
```html
<keep-alive include="News">
        <router-view></router-view>
</keep-alive>
```

### 路由组件两个新的生命周期

```html
<script>
export default {
  name: "News",
  mounted() {},
  // 路由组件在keep-alive包裹下才有的生命周期
  activated(){
    console.log('路由组件被激活了');
  },
  // 路由组件在keep-alive包裹下才有的生命周期
  deactivated(){
    console.log('路由组件被销毁了');
  }
};
</script>
```

⚠️ 注意：activated()和deactivated()只有在`<keep-alive></keep-alive>`包裹的时候才有效。因为在`<keep-alive></keep-alive>`中，我们正常的钩子函数就没办法执行了，这个时候`activated()`和`deactivated()`就会执行。

### 全局前置路由守卫和全局后置路由守卫
什么是路由守卫❓
说白了就是像「拦截器」的东西，在这里面可以做一些组件跳转前或组建跳转后的逻辑处理（比如用户身份鉴权）

**全局前置路由守卫**会在每一个路由组件被展示前调用，这时候可以在路由守卫里面去做一些js逻辑判断，来确保路由组件是不是真的要展示给用户看。

**全局后置路由守卫**是在路由组件被展示给用户看后才调用的

**代码模版：**

在`router`文件夹📁下的`index.js`中配置


```javascript
import ......
// 创建并暴露一个路由器
const router =  new VueRouter({
    	......	
})

// 前置路由守卫
router.beforeEach((to,from,next)=>{
    // meta字段下面会讲
    if(to.meta.isAuth){
        console.log('需要鉴权')
        // 这里省略一百万行鉴权代码
        next()
    }else{
        next()
    }
})

// 后置路由守卫
router.afterEach((to,from)=>{
	......
})

export default router
```
**前置路由守卫**里面写的是一个回调函数，回调函数能接收到三个参数，分别是`(to,from,next)`，to能够展示路由去向，from能够展示路由来源，next是一个方法，让路由组件在前置路由守卫中处理完逻辑后能够继续走下去，展示to里面指向的路由组件
![在这里插入图片描述](https://img-blog.csdnimg.cn/bb5290a4e7304abdbfc713da7d55f3b8.png)

**全局后置路由守卫**同上，只是没有next参数

### 路由配置中的meta字段
meta字段能够在路由组件切换的过程中，传递用户的「元数据」，就是用户的「自定义」数据。这个数据可以供路由守卫鉴权用。
```javascript
export default new VueRouter({
	routes:[
		{
			name:'home',
            path:'/home',
            component:Home,
            // 路由配置中的meta字段
            meta:{isAuth:true},
		}
	]
})
```

### 独享路由守卫
代码模版：

在`router`文件夹📁下的`index.js`中配置

```javascript
// 创建并暴露一个路由器
const router =  new VueRouter({
    routes:[
        {
            name:'home',
            path:'/home',
            component:Home,
			// 独享路由守卫
            beforeEnter:(to,from,next)=>{
                console.log('/home的独享路由守卫被调用')
                next()
            }
        }
    ]
})
```
### 组件内路由守卫
在路由组件里编写的路由守卫
```javascript
<script>
export default {
  name: "Home",
  components: {},
  methods: {

  },
  // 组件内守卫
  // 通过路由规则，进入该组件时被调用
  beforeRouteEnter: (to, from, next)=>{
    next()
  },
  // 通过路由规则，离开该组件时被调用
  beforeRouteLeave: (to, from, next)=> {
    next()
  }
};
</script>
```
### 修改路由模式
将`hash`模式改成`history`

在`router`文件夹📁下的`index.js`中配置
```javascript
// 创建并暴露一个路由器
const router =  new VueRouter({
	// 将`hash`模式改成`history`
    mode:'history',
    routes:[
        ......
    ]
})
```

