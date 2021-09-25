# 一些Vue起步需要知道的小知识
### {{xxx}}插值语法
##### 起步代码：

```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<!-- 引入Vue -->
		<script src="js/vue.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<!-- 准备一个容器 -->
		<div id="root">
			<h1>{{name}}</h1>
		</div>
		<script type="text/javascript">
			//创建Vue实例
			new Vue({
				el:"#root", // el用于指定当前Vue为哪个容器服务
				data:{
					name:"起步代码"
				}
			})
		</script>
	</body>
</html>
```

 - 想要Vue工作，就必须创建一个Vue实例，并且传入一个配置对象
 - root容器里面的代码被称为「Vue模板」
 - {{xxx}}里面可以撰写JS表达式，不一定是data里面定义的
 - **Vue实例和容器是一一对应的**
 - **真实开发中只会有一个Vue实例，并且会配合着组件一起使用**
 
##### 注意区分JS代码和JS表达式
 - 表达式：一个表达式会生成一个值，可以放在任何一个需要值的地方；JS表达式是一种特殊的JS代码
 - 代码：
 	- for(){}
 	- if(){}

### v-bind指令语法

```html
	<body>
		<!-- 准备一个容器 -->
		<div id="root">
			<a :href="address">MyPage</a>
		</div>
		<script type="text/javascript">
			//创建Vue实例
			new Vue({
				el:"#root", // el用于指定当前Vue为哪个容器服务
				data:{
					name:"起步代码",
					address:'https://www.chuanyangchen.ink'
				}
			})
		</script>
	</body>
```

v-bind 可以用：代替，且`:href="xxx"`中`xxx`写的依旧是JS表达式
**什么时候用插值语法？什么时候用指令语法？**
- 插值语法用于解析「标签体」内容
- 指令语法用于解析「标签」（包括🏷️标签熟悉，标签体内容，绑定事件）

### 数据绑定
##### Vue中有2种数据绑定的方式：

```html
单向数据绑定 <input type="text" :value = "name"><br/>
双向数据绑定 <input type="text" v-model = "name"><br/>
```

- 单向绑定🔌（v-bind）：数据只能从data流向页面
- 双向绑定🔗（v-model）：页面数据和data数据联动

备注：

 - 双向绑定一般都应用在表单类元素上（input，select等）
 - v-model默认收集的就是value值

