# 简述JavaScript中的Object.defineProperty()

#### 理解Vue的VM模型必备
----
#### 笔记内容
 - 前言
 - 不可枚举解决办法
 - 新定义的属性值不可修改解决办法
 - 新定义的属性值不可删除解决办法
 - get()函数
 - get()函数
----
## 前言
Object.defineProperty()的作用就是直接在一个对象上定义一个新属性，或者修改一个已经存在的属性，示例代码如下：

```javascript
Object.defineProperty(obj, prop, desc)
```
- obj：需要定义属性的对象名
- prop：定义的属性名
- desc：属性描述

## 情况举例：不可枚举

```javascript
<script type......>
let person = {
				name:"Mike",
				sex:'man'
			}
			Object.defineProperty(person,'age',{
				value:18
			})
			console.log(person);
......
```
控制台输出结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/891b3d49357246139e44af4b16612e65.png)尝试枚举person对象

```javascript
<script type="text/javascript">
			let person = {
				name:"Mike",
				sex:'man'
			}
			Object.defineProperty(person,'age',{
				value:18
			})
			console.log(Object.keys(person))
......
```

控制台输出结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/e1f7459fc9f34f2897f0271b9d14d39c.png)
**如何解决不可枚举的问题呢**

```javascript
......
Object.defineProperty(person,'age',{
				value:18,
				enumerable:true
			})
......
```

控制台输出：
![在这里插入图片描述](https://img-blog.csdnimg.cn/23a0a46b65ea4ad79d1d3193e3ece108.png)
## 情况举例：属性值不可修改
如果只是像这样描述新定义的属性的话，是没办法修改新添加属性值的
```javascript
......
Object.defineProperty(person,'age',{
				value:18,
				enumerable:true
			})
			person.age = 19;
			console.log(person);
......
```



控制台输出：
![在这里插入图片描述](https://img-blog.csdnimg.cn/2f2cf68df2514a289caeed852a9e0d78.png)

**解决办法**

```javascript
Object.defineProperty(person,'age',{
				value:18,
				writable:true
			})
			person.age = 19;
			console.log(person);
```
控制台输出：
![在这里插入图片描述](https://img-blog.csdnimg.cn/3019d845b7de41df8b9bed0028204d36.png)
### 情况举例：属性值不可删除
##### 像如上代码所定义的age属性，是不能通过delete删除的，这里不再过多描述不可删除的情况🙅‍♂️

**解决办法**

```javascript
Object.defineProperty(person,'age',{
				value:18,
				configurable:true
			})
			delete person.age
			console.log(person);
```

控制台输出：
![在这里插入图片描述](https://img-blog.csdnimg.cn/98250e2114f34bf68572ba54b52eaad1.png)
## 总结
--------
enumerable:true, // 控制属性是否可以被枚举
				writable:true, // 控制属性是否可以被修改
				configurable:true // 控制属性是否可以被删除

---

```javascript
<script type="text/javascript">
			let number = 18
			let person = {
				name:"Mike",
				sex:'man'
			}
			Object.defineProperty(person,'age',{
				get(){
					console.log('get()被访问')
					return number;
				},
				set(value){
					console.log('set()被访问')
					number = value;
				}
			})
			console.log(person.age) //输出age值
			person.age = 23 // 修改age值
			console.log(person.age)
......
```
控制台输出：
![在这里插入图片描述](https://img-blog.csdnimg.cn/17d34bfd673c4305ac9e0192cd14d3ca.png)



