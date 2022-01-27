# Vue中插件plugin的使用方法
基础作用：插件可以整合项目中Vue所有的全局定义
#### 用法：
在项目src目录下创建一个`plugin.js`的文件 📃
![在这里插入图片描述](https://img-blog.csdnimg.cn/2707e58029d1471a8ac85369757151fa.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
代码示例：
```javascript
export default{
    install(Vue){
        // 定义全局过滤器
        Vue.filter('过滤器名称',function(value){
            
        })

        // 定义全局指令
        Vue.directive('fbind', function (el, binding) {
            
        });

        // 定义混入
        Vue.mixin();

        // 给Vue原型上添加一个方法
        Vue.prototype.hello = ()=>{
            alert("hello");
        }
    }
}
```
在`main.js`中，导入插件，以便项目全局可以使用
![在这里插入图片描述](https://img-blog.csdnimg.cn/87612b8c41194a608e302b359ada8f25.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
代码示例：
```javascript
import plugins from './plugin'
Vue.use(plugins)
```

