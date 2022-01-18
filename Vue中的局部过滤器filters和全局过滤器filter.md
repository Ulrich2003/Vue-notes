# Vue中的局部过滤器filters和全局过滤器filter

##### 过滤器的定义：

对要显示的数据进行特定的格式化后再显示（适用于一些简单的逻辑处理）

##### 语法：

- 注册过滤器：Vue.filter(name, callback) 或 new Vue( filters:{} ) 
- 使用过滤器：{{ xxx | 过滤器名 }} 或 v-bind: 属性 = "xxx | 过滤器名"

##### 备注：

- 过滤器也可以接收额外参数，多个过滤器也可以串联
- 并没有改变原本的数据，而是产生新的对应的数据

#### 全局过滤器

![image-20220118093418057](https://vichien-public.oss-cn-guangzhou.aliyuncs.com/typora/image-20220118093418057.png)

#### 局部过滤器

![image-20220118093508049](https://vichien-public.oss-cn-guangzhou.aliyuncs.com/typora/image-20220118093508049.png)

#### 过滤器的参数：

```vue
{{time | timeFormater()}}
解析：time 作为参数 传递给 timeFormater()
```

![image-20220118093923498](https://vichien-public.oss-cn-guangzhou.aliyuncs.com/typora/image-20220118093923498.png)

#### 附录 （测试代码）：

```vue
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <script src="./js/vue.js"></script>
	<script src="https://cdn.bootcdn.net/ajax/libs/dayjs/1.10.7/dayjs.min.js"></script>
</head>
<body>
	<div id="main">
		现在的Unix时间戳(Unix timestamp)是 {{time | timeFormater()}}<br><br>
		现在被截取的的Unix时间戳是 {{time | timeFormater('YYYY_MM_DD') | mySlice() }}
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
			time:1642468041
		},
		methods:{
			
		},
		// 局部的过滤器
		filters:{
			timeFormater(value,str = 'YYYY 年 MM 月 DD 日 '){
				return dayjs(value).format(str);
			}
		}
	})
</script>

<style>
</style>

```

