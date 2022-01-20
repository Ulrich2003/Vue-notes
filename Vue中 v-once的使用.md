# Vue中 v-once的使用

1. v-once所在节点在初次动态谊染后，就视为静态内容了。

2. 以后数据的改变不会引起v-once所在结构的更新，可以用于优化性能。

![image-20220120164532780](https://vichien-public.oss-cn-guangzhou.aliyuncs.com/typora/image-20220120164532780.png)

#### 测试代码：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <script src="./js/vue.js"></script>
</head>
<body>
	<div id="main">
		<h2 v-once>the initialization of n is {{n}}</h2>
		<h2>the current value of n: {{n}}</h2>
		<button type="button" @click="addn()">click I let n plus 1</button>
	</div>
</body>
</html>

<script>
	// 全局过滤器
	Vue.filter('mySlice',function(value){
		return value.slice(0,4); 
	})

	var vm = new Vue({
		el:"#main",
		data:{
			n:1
		},
		methods:{
			addn(){
				this.n++;
			}
		}
	})
</script>

<style>
</style>

```

