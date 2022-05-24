# vue路由router的props配置

前置知识：[vue-router3路由配置和使用，适配vue2，vue-router代码模版](https://blog.csdn.net/weixin_45525653/article/details/124948059?spm=1001.2014.3001.5501)

**路由props配置的作用：让路由组件更方便的接收到参数**

⚠️ 当不使用props配置，组件拿到路由传递过来的参数需要这么写，组件里面出现非常多的`$route.query`或`$route.params`的字样：
![在这里插入图片描述](https://img-blog.csdnimg.cn/ed8d1a7cc0ad43fea057ce0233722428.png)

### 如何配置路由的props
说到配置路由，肯定是去`router`文件夹下的`index.js`中去写点代码

```javascript
export default new VueRouter({
    routes:[
        {
            name:'about',
            path:'/about/:content',
            component:About,
            // 第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给組件
            // 一般不会使用这种写法，因为数据写死在路由配置里面
            // props:{content:'这里是「关于我们」页面'}

            // 第二种写法：当props收到bool值为true时，则把路由收到的所有params参数通过props传给組件
            // 这种做法也有局限性，query中的值就死活读不到了
            // props:true

            // 第三种写法：props值为函数，该函数返回所有的key-value的组合都会通过props传给組件
            // 这个做法的优点是既能够收params参数又可以收query参数
            props(route){
                return {
                    paramsContent:route.params.content,
                    id:route.query.id
                }
            }
        },
    ]
})
```

### 配置完后，该如何在组件里面拿到参数呢
![在这里插入图片描述](https://img-blog.csdnimg.cn/99d5f7a7a7964db3ba0d875a6b0ae536.png)

