前置知识：
[Vue组件间的数据传递](https://blog.csdn.net/weixin_45525653/article/details/122704736?spm=1001.2014.3001.5501)
需要搞懂这一篇文章后，才能看懂下面的内容👇

#### 需求：
工程目录如下：
![在这里插入图片描述](https://img-blog.csdnimg.cn/ac2e7c54afbf46dda50406c5632ba99d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_9,color_FFFFFF,t_70,g_se,x_16)
#### 目录
##### 利用props传递：
实现在School.vue组件内，点击一个按钮🔘，将学校名传到App.vue组件中。
##### 组件自定义事件：利用 v-on 和 ref 传递
实现在Student.vue组件内，点击一个按钮🔘，将学生名传到App.vue组件中。

----
[GitHub：本项目源码下载直通车 ⏬](https://github.com/Ulrich2003/Vue-notes/releases/tag/1.0)
![在这里插入图片描述](https://img-blog.csdnimg.cn/bcf2b8ccfb19433f833a6d0e102cc712.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
### 利用props传递：
实现在School.vue组件内，点击一个按钮🔘，将学校名传到App.vue组件中。
**School.vue 组件**
![在这里插入图片描述](https://img-blog.csdnimg.cn/3bb22d3118124e889e1be831cf8f7dcf.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
**App.vue 组件**
![在这里插入图片描述](https://img-blog.csdnimg.cn/9871212271be49b0a3d89a319424b596.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
School.vue 代码：
```html
<template>
    <div>
        <div>The School Name: {{name}}</div>
        <button @click="sendSchoolName">点我将学校名传给APP</button>
    </div>
</template>

<script>
export default {
    name:'School',
    props:['getSchoolName'],
    data(){
        return {
            name:"NTU"
        }
    },
    methods:{
        sendSchoolName(){
            this.getSchoolName(this.name);
        }
    }
}
</script>
```
## 组件自定义事件：利用 v-on 和 ref 传递
实现在Student.vue组件内，点击一个按钮🔘，将学生名传到App.vue组件中。
##### 利用v-on传递：
**App.vue 组件**
![在这里插入图片描述](https://img-blog.csdnimg.cn/ce8fdb1649d249c2bb5b3754ea89a166.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
**Student.vue 组件**
![在这里插入图片描述](https://img-blog.csdnimg.cn/d4f5ec4ac2444f87aa15afa903cbe324.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
**Student.vue 代码**

```html
<template>
  <div>
    <div>The Student Name: {{ name }}</div>
    <div>Age: {{ age }}</div>
    <button @click="sendStudentName">点我将学生名传给APP</button>
  </div>
</template>

<script>
export default {
  name: "Student",
  data() {
    return {
      name: "Ulrich",
      age: 22,
    };
  },
  methods:{
      sendStudentName(){
          this.$emit('NTU', this.name);
      }
  }
};
</script>
```
##### 利用 ref 传递
实现在Student.vue组件内，点击一个按钮🔘，将学生名传到App.vue组件中。
这种方式可以让自定义事件变得更加灵活。

**Student.vue 代码同上**

```html
<template>
  <div>
    <div>The Student Name: {{ name }}</div>
    <div>Age: {{ age }}</div>
    <button @click="sendStudentName">点我将学生名传给APP</button>
  </div>
</template>

<script>
export default {
  name: "Student",
  data() {
    return {
      name: "Ulrich",
      age: 22,
    };
  },
  methods:{
      sendStudentName(){
          this.$emit('NTU', this.name);
      }
  }
};
</script>
```
**App.vue 组件**
![在这里插入图片描述](https://img-blog.csdnimg.cn/ec33b63719fb440f8e8513d941dfed14.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
**App.vue 代码**

```html
<template>
  <div id="app">
    <School :getSchoolName="getSchoolName"></School>
    <Student @NTU="getStudentName"></Student>
    <Student ref="student"></Student>
  </div>
</template>

<script>
import Student from './components/Student.vue'
import School from './components/School.vue'

export default {
  name: 'App',
  components: {
    Student,
    School
  },
  methods:{
    getSchoolName(name){
      console.log('App得到学校名:'+name);
    },
    getStudentName(name){
      console.log('APP得到学生名:'+name);
    }
  },
  mounted(){
    setTimeout(() => {
      // 让页面加载完3秒后才允许触发该事件
      this.$refs.student.$on('NTU',this.getStudentName)
    }, 3000);
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 10px;
  margin-left: 10px;
  font-size: 30px;
  font-weight: bold;
}
</style>

```

