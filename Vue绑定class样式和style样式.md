# Vue绑定class样式和style样式
### 绑定class样式
`:class`里面包含的是表达式，可以获取到data里面定义的属性。
```html
<style>
	div{
		width: 500px;
		height: 500px;
	}
	.default{
		border: chocolate 1px solid;
	}
	.blue{
		background-color: cornflowerblue;
	}
	.orange{
		background-color: orange;
	}
	</style>
  <body>
    <!-- 准备一个容器 -->
    <div id="root">
      <div class="default" :class="color" @click="changeColor"></div>
    </div>
    <script type="text/javascript">
      //创建Vue实例
      const vm = new Vue({
        el: "#root",
        data: {
          color : "blue"
        },
        methods: {
			changeColor(){
				this.color = "orange"
			}
		},
      });
    </script>
  </body>
```
### 绑定style样式
存在「-」的css属性，需要用驼峰命名的方式写入到data中

```html
 <body>
    <!-- 准备一个容器 -->
    <div id="root">
      <div class="default" :style="divStyle"></div>
    </div>
    <script type="text/javascript">
      //创建Vue实例
      const vm = new Vue({
        el: "#root",
        data: {
			divStyle:{
				width:'500px',
				height:'500px',
				backgroundColor:'red'
			}
        }
      });
    </script>
  </body>
```

