# Vue 中的自定义指令directive

⚠️ 自定义指令定义时需要注意的问题：

1. 可以是**对象**的形式，也可以是**函数**的形式
2. 不靠返回值改变目标值，靠传入的element 和 binding 改变目标值（操作DOM）
3. element是真实的DOM元素，不是虚拟DOM元素，binding是绑定元素的对象
4. 自定义函数调用时期：（1）指令与元素成功绑定时（页面一上来做的事情）（2）指令所在的模板被重新解析时
### 局部指令的定义
在「Vue对象」里面里使用`directives:{ 函数 or 对象 }`定义全局指令
![在这里插入图片描述](https://img-blog.csdnimg.cn/bc6b7387099a48329af23111361b4c13.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)

### 全局指令的定义
在`<script>`里使用`Vue.directive('指令名', 对象or函数)`定义全局指令
![在这里插入图片描述](https://img-blog.csdnimg.cn/288f4c81beba4328825cd27fd48a0676.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)

### * 附录（测试代码）

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <script src="./js/vue.js"></script>
</head>
<body>
	<div id="main">
		<h2>The current n value is <span v-text="n"></span></h2>
		<h2>Enlarge ten times the value of n is <span v-big="n"></span></h2>
		<button @click="n++">Click me, the value of n plus one</button>
		<hr >
		<input v-fbind:value="n"/>
	</div>
</body>
</html>

<script>
	// 全局指令
	Vue.directive('big',function(element,binding){
		element.innerText = binding.value * 10;
	})
	
	Vue.directive('fbind',{
		// 对象中的这三个函数名字是特定的，不能写错名字
		// bind()中的内容往往是和update()中的内容是重复的，所以才有以上函数调用的形式
		bind(element,binding){ // 指令和元素成功绑定时（一上来）
			element.value = binding.value;
			console.log("bind")
		},
		inserted(element,binding){ // 指令所在元素被插入页面时
			element.focus();
			console.log("inserted")
		},
		update(element,binding){ // 指令所在模板被重新解析时
			element.value = binding.value;
			console.log("update")
		}
	})
	
	var vm = new Vue({
		el:"#main",
		data:{
			n:1
		},
		methods:{
			
		},
		directives:{ // 局部指令
			// 可以是对象的形式，也可以是函数的形式
			// 不靠返回值改变目标值，靠改变收到的a和b改变目标值
			// element是真实DOM元素，binding是绑定的元素的对象
			// big函数调用的时机：1.指令与元素成功绑定时（一上来）2.指令所在的模板被重新解析时
			big(element,binding){
				element.innerText = binding.value * 10;
			},
			fbind:{
				// 对象中的这三个函数名字是特定的，不能写错名字
				// bind()中的内容往往是和update()中的内容是重复的，所以才有以上函数调用的形式
				bind(element,binding){ // 指令和元素成功绑定时（一上来）
					element.value = binding.value;
					console.log("bind")
				},
				inserted(element,binding){ // 指令所在元素被插入页面时
					element.focus();
					console.log("inserted")
				},
				update(element,binding){ // 指令所在模板被重新解析时
					element.value = binding.value;
					console.log("update")
				}
			}
		}
	})
</script>

<style>
</style>

```

