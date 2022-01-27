# Vue中mixin混入的使用
#### 1. 创建一个js文件，里面写着可以混入使用的代码
![在这里插入图片描述](https://img-blog.csdnimg.cn/1ca491d37d554d0a856279aa14294ee0.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_11,color_FFFFFF,t_70,g_se,x_16)
里面写着可以混合复用的代码：
![在这里插入图片描述](https://img-blog.csdnimg.cn/380dc69cb5024c0da3c449b34e6bdc16.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
#### 2. 使用这个js文件进行混入
##### 局部混入
在组件中使用 `import` 导入步骤一编写的JS文件
使用`mixins:[...]`进行混入
![在这里插入图片描述](https://img-blog.csdnimg.cn/8d8dbe71d5e1409b80db56c026367c44.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)
##### 全局混入
直接在main.js里面编写以下语句，即可进行全局混入
![在这里插入图片描述](https://img-blog.csdnimg.cn/46ea3bba34204507be630be5d7752536.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAQ2h1YW5ZYW5nIENoZW4=,size_20,color_FFFFFF,t_70,g_se,x_16)

