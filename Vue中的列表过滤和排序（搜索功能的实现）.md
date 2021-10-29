# Vue中的列表过滤和排序（搜索功能的实现🔍）
### 使用watch实现列表过滤

```html
...
<body>
	<div id="div1">
		<input v-model="keyword">
		<ul>
			<li v-for="(p,index) in filPersons" :key="p.id">
				{{p.name}} - {{index}}
			</li>
		</ul>
	</div>
</body>
</html>

<script>
	var vm = new Vue({
		el:"#div1",
		data:{
			keyword:'',
			persons:[
				{id:'001',name:'李明',gender:'男'},
				{id:'002',name:'明柯',gender:'女'},
				{id:'003',name:'柯诺',gender:'男'},
				{id:'004',name:'诺行',gender:'女'}
			],
			filPersons:[]
		},
		watch:{
			keyword:{
				immediate:true,
				handler(val){
					this.filPersons = this.persons.filter((p)=>{
					return p.name.indexOf(val)!==-1
					})
				}
			}
		}
	})
</script>
```
#### 效果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/a5cc7b925e874b7288ede0f120f853d2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_13,color_FFFFFF,t_70,g_se,x_16)

```html
...
<body>
	<div id="div1">
		<input v-model="keyword">
		<ul>
			<li v-for="(p,index) in filPersons" :key="p.id">
				{{p.name}} - {{index}}
			</li>
		</ul>
	</div>
</body>
</html>

<script>
	var vm = new Vue({
		el:"#div1",
		data:{
			keyword:'',
			persons:[
				{id:'001',name:'李明',gender:'男'},
				{id:'002',name:'明柯',gender:'女'},
				{id:'003',name:'柯诺',gender:'男'},
				{id:'004',name:'诺行',gender:'女'}
			]
		},
		computed:{
			filPersons(){
				return this.persons.filter((p)=>{
					return p.name.indexOf(this.keyword)!==-1
				})
			}
		}
	})
</script>
```
### 列表的排序

```html
...	
<body>
	<div id="div1">
		<input v-model="keyword">
		<button @click="sortType = 2">年龄升序</button>
		<button @click="sortType = 1">年龄降序</button>
		<button @click="sortType = 0">复位</button>

		<ul>
			<li v-for="(p,index) in filPersons" :key="p.id">
				{{p.name}} - {{p.age}}
			</li>
		</ul>
	</div>
</body>
</html>

<script>
	var vm = new Vue({
		el:"#div1",
		data:{
			keyword:'',
			sortType:0, // 0原顺序 1降序 2升序
			persons:[
				{id:'001',name:'李明',gender:'男',age:12},
				{id:'002',name:'明柯',gender:'女',age:14},
				{id:'003',name:'柯诺',gender:'男',age:22},
				{id:'004',name:'诺行',gender:'女',age:23}
			]
		},
		computed:{
			filPersons(){
				const arr =  this.persons.filter((p)=>{
					return p.name.indexOf(this.keyword)!==-1
				})
				// 判断是否需要排序
				if(this.sortType){
					arr.sort((p1,p2)=>{
						return this.sortType === 1 ? p2.age-p1.age : p1.age-p2.age
					})
				}
				return arr
			}
		}
	})
</script>
```

