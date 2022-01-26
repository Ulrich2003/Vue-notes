# 前言
本文讲解两个Vue的知识点：
- 给Vue组件传递数据的3种办法
- 如何修改传递给Vue组件数据的值
-------

## 给Vue组件传递数据的3种办法
- 在组件中利用数组简单声明接收（常用）
- 在组件中利用对象接收数据（2种比较高级的办法）

#### 1. 在组件中利用数组简单声明接收
在组件中，通过`props:['name','age','gender']`的方式接收需要从外部传递进来的字段
![在这里插入图片描述](https://img-blog.csdnimg.cn/43dcf92b696546daaa64d42223f15de5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
**在App.vue 中的写法（传递数据给组件）：**
![在这里插入图片描述](https://img-blog.csdnimg.cn/966541df5760472a928bb2bb2490fb4e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
#### 2.利用对象的方式限制传递的数据类型
![在这里插入图片描述](https://img-blog.csdnimg.cn/2a4b0537adcc4281912ded090a097bb5.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
⚠️ 下面展示传递错误的数据类型 ❌
![在这里插入图片描述](https://img-blog.csdnimg.cn/4c3497c2a36e44a39d3a022947e55ac0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
橙色方框内的传递方式，会被vue当成字符串处理，并不是Number类型的，绿色方框利用`:age="19"` 传递的数据，双引号中的19被认为是JS命令传递，类型可以被Vue认为是Number类型
在页面中，虽然能将传递的数据展示到页面上，但控制台会因为传递类型错误报错。
![在这里插入图片描述](https://img-blog.csdnimg.cn/bea91dc4c7bd4b6db83bec2e2fedcea2.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
#### 3. 利用对象的方式限制传递的数据类型+默认值的指定+必要性的限制
![在这里插入图片描述](https://img-blog.csdnimg.cn/c611a3156b504bdab990c0aa56a618fd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
**在App.vue 中的写法（传递数据给组件）：**
![在这里插入图片描述](https://img-blog.csdnimg.cn/a58fdb682bd14240bd00fc0d3f44864f.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
**页面展示：**
![在这里插入图片描述](https://img-blog.csdnimg.cn/f538a0b1be90492d969ad10fe0771a20.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
## 如何修改传递给Vue组件的数据的值
在Vue中这种做法是不允许的 ❎，这意味着我们没办法直接修改传递进组件的数据。

⚠️ 下面展示传递错误的写法 ❌
![在这里插入图片描述](https://img-blog.csdnimg.cn/1eab7cea760043bcb7a4c3fbd128baca.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)

如果我们非要这么做，页面确实会展示+1后的数据，但控制台会报错。
![在这里插入图片描述](https://img-blog.csdnimg.cn/f847e0a41c9d447d8d4ff04df6927c6b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
✅ 正确的写法是需要有一个中间变量`myAge`接收`age`值，通过修改`myAge`值来实现
![在这里插入图片描述](https://img-blog.csdnimg.cn/a4ebefdd51b6484e974e59df9494b706.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
**全剧终**
