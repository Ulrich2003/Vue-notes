# Vue中的监视属性watch以及深度监视、监视的简写形式
- 当被监视的属性发生变化时，回调函数自动掉用，进行相关操作
- 监视的属性必须存在，才能进行监视 🔭
- 监视的两种写法
-- new Vue时传入watch配置 
-- 通过vm.$watch监视
- `immediate:true`可以在初始化时让handler调用一下

### new Vue时传入watch配置 

```html
<body>
		<!-- 准备一个容器 -->
		<div id="root">
			姓<input type="text" v-model="firstname"><br/>
			名<input type="text" v-model="lastname"><br/>
		</div>
		<script type="text/javascript">
			//创建Vue实例
			new Vue({
				el:"#root", 
				data:{
					firstname:"Chen",
					lastname:"Chuanyang"
				},
				watch:{
					firstname:{
						handler(){
							console.log('firstname被修改成:'+this.firstname)
						}
					}
				}
			})
		</script>
	</body>
```

### 通过vm.$watch监视

```html
<body>
		<!-- 准备一个容器 -->
		<div id="root">
			姓<input type="text" v-model="firstname"><br/>
			名<input type="text" v-model="lastname"><br/>
		</div>
		<script type="text/javascript">
			//创建Vue实例
			const vm = new Vue({
				el:"#root", 
				data:{
					firstname:"Chen",
					lastname:"Chuanyang"
				}
			})

			vm.$watch('firstname',{
				immediate:true, // 初始化时让handler调用一下
				handler(){
					console.log('firstname修改成：'+this.firstname)
				}
			})

		</script>
	</body>
```

### 深度监视deep

```html
<script type="text/javascript">
      //创建Vue实例
      const vm = new Vue({
        el: "#root",
        data: {
          firstname: "Chen",
          lastname: "Chuanyang",
          numbers: {
            a: 88,
            b: 99,
          },
        },
        watch: {
          numbers: {
            deep: true, // 不写这一句是没法监视到a和b的单独变化的
            handler() {
              console.log("numbers改变了");
            }
          }
        }
      });
    </script>
```

### 监视的简写形式
前提要求：只简单监视属性的变动

```html
<body>
    <!-- 准备一个容器 -->
    <div id="root">
      <input type="text" v-model="firstname" />
      <input type="text" v-model="lastname" />
    </div>
    <script type="text/javascript">
      //创建Vue实例
      const vm = new Vue({
        el: "#root",
        data: {
          firstname: "Chen",
          lastname: "Chuanyang"
        },
        watch: {
          lastname(){
			  console.log('lastname修改了')
		  }
        }
      });
    </script>
  </body>
```

