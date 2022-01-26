# Vue单文件组件的编写和使用，需配合Vue手脚架使用
----- VUE手脚架的搭建这里不进行描述 -----
### 手脚架中需要关注的几个文件![在这里插入图片描述](https://img-blog.csdnimg.cn/7b41a21d7d3f4b7a9429a977ecde3d5a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
### 组件编写流程
- 编写单文件组件
- 编写App.vue
###  如何编写单文件组件：
🌰 以Student组件和Class组件编写为例：
Student组件的编写：

```html
<template>
	<!-- 组件在页面中展示的样式 -->
	<div>
		<h2>Name: {{name}}</h2>
		<h2>Age: {{age}}</h2>
		<h2>Gender: {{gender}}</h2>
	</div>
</template>

<script>
	export default {
		// 组件名称，一般和文件名相同
		name:"Student",
		// 组件里面不需要el配置项，最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器
		data(){ // data只能写成普通函数的形式
			return {
				name:"Joshua",
				age:17,
				gender:"Man"
			}
		}
	}
</script>

<style>
	
</style>

```
Class组件的编写：

```html
<template>
	<div>
		<h2>ClassNum: {{classNum}}</h2>
	</div>
</template>

<script>
	// export default 是指默认暴露
	export default{
		name:"Class",
		// 组件里面不需要el配置项，最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器
		data(){ // data只能写成普通函数的形式
			return {
				classNum:"Joshua",
			}
		}
	}
</script>

<style>
	
</style>

```
### 编写App.vue
App.vue 也是一个单文件组件，但它和其他组件不相同，它只负责管理所有的.vue组件

```c
<template>
	<div>
		<Student/>
		<Class/>
	</div>
</template>

<script>
	// 引入组件
	import Student from './components/Student.vue'
	import Class from './components/Class.vue'
	
	export default {
		name:'App',
		components:{
			Student,
			Class
		}
	}
</script>

<style>
	
</style>

```

**至此，组件编写的流程大致就结束咯**
### 脚手架运行效果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2b1ddcd418d346249e2023cc5cabb1ab.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_19,color_FFFFFF,t_70,g_se,x_16)

