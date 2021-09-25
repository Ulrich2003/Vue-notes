# Vue中el和data的两种使用方式
### el的两种写法 （不是很重要⚠️）
##### el最基本的使用方式：
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
##### 利用$mount将数据“放/挂载”到root上去
```html
	<body>
		<!-- 准备一个容器 -->
		<div id="root">
			<a :href="address">MyPage</a>
		</div>
		<script type="text/javascript">
			//创建Vue实例
			const x = new Vue({
				data:{
					name:"起步代码",
					address:'https://www.chuanyangchen.ink'
				}
			})
			x.$mount("#root")
		</script>
	</body>
```
### data的两种写法 （非常重要❗️❗️）
##### 对象式写法：
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
##### 函数式写法：
要求函数一定要返回🔙一个对象

```html
	<body>
		<!-- 准备一个容器 -->
		<div id="root">
			<a :href="address">MyPage</a>
		</div>
		<script type="text/javascript">
			//创建Vue实例
			new Vue({
				el:"#root", 
				data(){
				// 或写成data:function(){
					return {
						name:"起步代码",
						address:'https://www.chuanyangchen.ink'
					}
				}
			})
		</script>
	</body>
```

