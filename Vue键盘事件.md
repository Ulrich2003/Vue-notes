# Vue键盘事件 ⌨️
vue中常见的按键别名

 - 回车	enter
 - 删除	delete
 - 退出	esc
 - 空格 space
 - 换行	tab（特殊，必须用keydown）
 - 上	up ⬆️
 - 下	down ⬇️
 - 左	left ⬅️
 - 右	right ➡️

#### enter键盘事件示例：
```html
<body>
		<!-- 准备一个容器 -->
		<div id="root">
			<input type="text" placeholder="按下回车提示输入" @keydown.enter="showInfo">
		</div>
		<script type="text/javascript">
			//创建Vue实例
			new Vue({
				el:"#root", 
				data:{
					
				},
				methods:{
					showInfo(e){
						console.log(e.target.value)
					}
				}
			})
		</script>
	</body>
```

