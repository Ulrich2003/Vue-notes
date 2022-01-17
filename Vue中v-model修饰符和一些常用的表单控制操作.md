# Vue中v-model修饰符和一些常用的表单控制操作

### 表单提交操作：@submit 和 prevent

@submit可以在表单提交瞬间触发相对应的方法，prevent修饰符可以阻止表单提交操作时的「默认事件」，比如“刷新”

![image-20220117143122250](https://vichien-public.oss-cn-guangzhou.aliyuncs.com/typora/image-20220117143122250.png)

### v-model.trim 和 v-model.number 和 v-model.lazy 的使用

#### v-model.trim 

去除用户输入的 “字符串” 前的空格和 “字符串” 后面的空格

#### v-model.number

让用户输入的内容被Vue视为数字，这里需要注意以下内容 ⚠️ 👇

```html
<!-- type="number"是控制输入时只能输入数字 -->
<!-- v-model.number="..."是控制输入的内容被Vue视为数字（默认是字符串） -->
年龄：<input v-model.number="student.age" type="number" />
```

**type="number" 和 v-model.number="..." 这两个的作用完全不一样**

#### v-model.lazy

lazy可以让vue失去焦点的一瞬间再收集数据，而不是输入一个字符，vue就立刻读取到收集的内容。

![image-20220117143836259](https://vichien-public.oss-cn-guangzhou.aliyuncs.com/typora/image-20220117143836259.png)

### 对象转JSON字符串

```javascript
JSON.stringify(对象名);
```

![image-20220117144012205](https://vichien-public.oss-cn-guangzhou.aliyuncs.com/typora/image-20220117144012205.png)

### 附录 （测试代码）

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <script src="./js/vue.js"></script>
</head>
<body>
	<div id="main">
		<!-- 表单提交时触发submit()方法，并且阻止默认事件(刷新) -->
		<form @submit.prevent="submit()">
			姓名：<input v-model.trim="student.name" type="text" /><br /><br />
			<!-- type="number"是控制输入时只能输入数字 -->
			<!-- v-model.number="..."是控制输入的内容被Vue视为数字（默认是字符串） -->
			年龄：<input v-model.number="student.age" type="number" /><br /><br />
			班级：<input v-model="student.class" />
			<!-- lazy可以让vue失去焦点的一瞬间再收集数据 -->
			备注：<input v-model.lazy="student.other"/>
			<!-- button默认type类型是submit -->
			<button>提交表单</button>
		</form>
	</div>
</body>
</html>

<script>
	var vm = new Vue({
		el:"#main",
		data:{
			student:{
				name:'',
				age:'',
				class:'',
				other:''
			}
		},
		methods:{
			submit(){
				// 将对象转化为JSON字符串的方法
				console.log(JSON.stringify(this.student));
			}
		}
	})
</script>

<style>
</style>

```

