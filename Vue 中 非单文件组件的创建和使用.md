# Vue 中 非单文件组件的创建和使用

#### 组件的创建分为三个步骤：

- 创建组件
- 注册组件
- 使用组件

#### 创建组件和注册组件的方式：

⚠️ 组件里面一定不要有el配置项，最终所有组件都要被一个vm管理，由vm决定服务于哪个容器

⚠️ data只能写成普通函数的形式，不能写成对象的形式（解释起来有点麻烦，有比较好解释的朋友评论区分享一下）

![image-20220123114905900](https://vichien-public.oss-cn-guangzhou.aliyuncs.com/typora/image-20220123114905900.png)

#### 使用组件：

在html标签内使用 **<组件名></组件名>** 的方式使用组件

### 附录（测试代码）

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <script src="./js/vue.js"></script>
</head>
<body>
	<div id="main">
		<student></student>
		<hr >
		
	</div>
</body>
</html>

<script>
	// 创建组件
	const student = Vue.extend({
		// 组件里面不需要el配置项，最终所有的组件都要被一个vm管理，由vm决定服务于哪个容器
		data(){ // data只能写成普通函数的形式
			return {
				name:"Joshua",
				age:17,
				gender:"Man"
			}
		},
		template:`
			<div>
				<h2>Name: {{name}}</h2>
				<h2>Age: {{age}}</h2>
				<h2>Gender: {{gender}}</h2>
			</div>
		`
	})
	// 全局注册组件
	Vue.component('student',student);
	
	var vm = new Vue({
		el:"#main",
		components:{ // 局部注册组件
			student
		}
	})
</script>
```

