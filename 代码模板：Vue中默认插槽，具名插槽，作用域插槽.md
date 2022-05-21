# Vue中默认插槽，具名插槽，作用域插槽
🔗 来源参考：尚硅谷Vue视频

### 如何理解插槽
大白话来讲，插槽相当于在自定义组件标签`<MyComponent> </MyComponent>`的中间写入（插入）html结构，把这些html结构传递到自定义组件中。当然，子组件也需要声明接收传入结构的摆放位置，让自定义组件知道如何将这些html结构摆放到页面中去。

### 默认插槽
```html
父组件：
	<MyComponent>
		<div>这里插入的是html结构</div>
	</MyComponent>

子组件：
	<template>
		<div>
			<slot>这里展示的是插槽的默认值，当父组件没有传入具体的结构时，会展示默认值的内容</slot>
		</div>
	</template>
```
默认插槽只能

### 具名插槽

```html
父组件：
	<MyComponent>
		<template slot="center">
			<div>这里插入的是html结构</div>
		</template>
		 <!-- 下面的写法是官方推荐的新写法 -->
		<template v-slot:footer>
			<div>这里插入的也是html结构</div>
		</template>
	</MyComponent>
子组件：
	<template>
		<div>
			<slot name="center">插槽默认内容...</slot>
			<slot name="footer">插槽默认内容...</slot>
		</div>
	</template>
```

### 作用域插槽：
什么时候会用到作用域插槽❓
数据在组件的自身，但根据数据生成的结构需要组件的使用者（父组件）来决定

```html
父组件：
	<MyComponent>
		<template scope="scopeData">
			<ul>
				<li v-for="g in scopeData.games" :key="g">{{g}}</li>
			</ul>
		</template>
	</MyComponent>
	<MyComponent>
		<template slot-scope="scopeData">
			<h4 v-for="g in scopeData.games">{{g}}</h4>
		</template>
	</MyComponent>
子组件：
	<template>
		<div>
			<slot :games="games"></slot>
		</div>
	</template>

	<script>
		export default{
			name:"MyComponent",
			// 数据在子组件自身
			data(){
				return {
					games:['CS','CF','洛克王国','赛尔号']
				}
			}
		}
	</script>
```

