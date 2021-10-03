# Vue的计算属性computed及计算属性的简写形式
- 计算属性的定义：要用的属性不存在，要通过已有属性计算🧮得来
- 原理：底层借助了Object.defineproperty方法提供的getter和setter
- 优势：与methods相比，内部有缓存机制（复用），效率更高，调试方便
-  get什么时候调用？？
-- 1.初次读取fullName时 
-- 2.所依赖的数据发生变化时
```html
<body>
		<!-- 准备一个容器 -->
		<div id="root">
			姓<input type="text" v-model="firstname"><br/>
			名<input type="text" v-model="lastname"><br/>
			全名：<span>{{fullname}}</span>
		</div>
		<script type="text/javascript">
			new Vue({
				el:"#root", 
				data:{
					firstname:"Chen",
					lastname:"Chuanyang"
				},
				methods:{
					
				},
				computed:{
					fullname:{
						 get(){
							 return this.lastname+' '+this.firstname;
						 }
					}
				}
			})
		</script>
	</body>
```
# computed的「简写形式」
- 注意⚠️：只能在考虑读取，不考虑修改computed内容时，才能使用简写形式

```html
<body>
		<!-- 准备一个容器 -->
		<div id="root">
			姓<input type="text" v-model="firstname"><br/>
			名<input type="text" v-model="lastname"><br/>
			全名：<span>{{fullname}}</span>
		</div>
		<script type="text/javascript">
			//创建Vue实例
			new Vue({
				el:"#root", 
				data:{
					firstname:"Chen",
					lastname:"Chuanyang"
				},
				methods:{
					
				},
				computed:{
					fullname(){
						return this.lastname+' '+this.firstname;
					}
				}
			})
		</script>
	</body>
```

