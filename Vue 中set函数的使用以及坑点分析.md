### Vue 中set() 函数的使用以及缺点分析

```javascript
this.$set(this.student,'gender','男');
this.$set(追加的对象名,'追加的字段名','追加的字段值');
```

以下代码展示的是点击按钮后为student对象追加一个性别属性：
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <script src="./js/vue.js"></script>
</head>
<body>
	<div id="main">
		<button @click="addGender">为Mike追加一个性别</button>
		<div>{{student.name}}</div>
		<div>{{student.age}}</div>
		<div>{{student.country}}</div>
		<div>{{student.gender}}</div>
	</div>
</body>
</html>

<script>
	var vm = new Vue({
		el:"#main",
		data:{
			student:{
				name:"Mike",
				age:19,
				country:"China"
			}
		},
		methods:{
			addGender(){
				this.$set(this.student,'gender','男');
			}
		}
	})
</script>
```
### 坑点分析：
无法直接给vm对象，或者是data对象加属性
官方：注意对象不能是 Vue 实例，或者 Vue 实例的根数据对象。

