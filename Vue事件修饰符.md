# Vue事件修饰符
prevent:阻止默认事件「常用」
				stop:阻止事件冒泡「常用」
				once:事件只触发一次「常用」
				capture:使用事件捕获模式
				self:只有evnet.target是当前操作的元素时才触发事件
```html
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<!-- 引入Vue -->
		<script src="js/vue.js" type="text/javascript" charset="utf-8"></script>
	</head>
	<body>
		<!-- 准备一个容器 -->
		<div id="root">
			<!-- 
				prevent:阻止默认事件「常用」
				stop:阻止事件冒泡「常用」
				once:事件只触发一次「常用」
				capture:使用事件捕获模式
				self:只有evnet.target是当前操作的元素时才触发事件
			 -->
			 <!-- 阻止默认事件
					描述：不阻止的话点击a标签显示提示信息后，还会继续跳转页面
			-->
			<a :href="address" @click.prevent="showInfo">MyPage</a>
			<!-- 阻止事件冒泡
					描述：不阻止的话，会显示两次alert信息
			-->
			<div @click="showInfo">
				<button @click.stop="showInfo">点我显示信息</button>
			</div>
			<!-- 事件只触发一次
					描述：点击按钮后弹窗一次alert，以后点击的时候不再弹窗
			-->
			<a :href="address" @click.once="showInfo">MyPage</a>
			<!-- 使用事件捕获模式
					描述：一般是先冒泡再处理相对应事件，capture能让事件在捕获阶段运行
					实现先捕获再冒泡
			-->
			<div style="background-color: bisque;padding: 20px;" @click.capture="showMsg(1)">
				div1
				<div style="background-color: chocolate;" @click="showMsg(2)">
					div2
				</div>
			</div>
			<!-- 只有evnet.target是当前操作的元素时才触发事件
					描述：这种方式也可以阻止冒泡
			-->
			<div style="background-color: bisque;padding: 20px;" @click.self="showMsg(1,event)">
				div1
				<div style="background-color: chocolate;" @click="showMsg(2,event)">
					div2
				</div>
			</div>
		</div>
		<script type="text/javascript">
			//创建Vue实例
			new Vue({
				el:"#root", 
				data:{
					name:"起步代码",
					address:'https://www.chuanyangchen.ink'
				},
				methods:{
					showInfo(){
						alert('Hello，CY')
					},
					showMsg(e,evnet){
						alert(e)
					}
				}
			})
		</script>
	</body>
</html>

```

