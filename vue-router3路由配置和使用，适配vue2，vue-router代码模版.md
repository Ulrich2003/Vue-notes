# vue-router3路由配置和使用，适配vue2，vue-router代码模版
### 前言
- 本文只适合vue2，不适合vue3，vue3对应的路由版本是vue-router@4

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

