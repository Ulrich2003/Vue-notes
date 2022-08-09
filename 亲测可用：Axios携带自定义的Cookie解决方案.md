# 亲测可用：Axios携带自定义的Cookie解决方案

做项目时遇到一个需求，后端需要在接口请求时，对用户登陆状态进行判断，需要在请求时携带Cookie。
**但是，Axios请求默认时不携带Cookie的**

## 解决方案：
1. 在`main.js`中添加以下代码：

```javascript
import axios from 'axios'
axios.defaults.withCredentials = true;
```

2. 在浏览器的Application中添加要携带的Cookie

![在这里插入图片描述](https://img-blog.csdnimg.cn/e13cb6f14f894c09803a8b7563ec0686.png)

## 踩坑记录
**无效的解决方案：**
直接在headers中加入“Cookie“ 并不能解决问题

```javascript
 axios({
    withCredentials: true,
    method: "post",
    url: "api/Admin/AuthManage/AuthHandler.ashx?t=954",
    headers: {
      "Content-Type": "application/x-www-form-urlencoded",
      "Cookie":'myCookie=83C13185E0......'
    },
    data: "BizContext=" + JSON.stringify(requestBodyData),
  })
    .then((res) => {
      ....
    })
    .catch((err) => {
      ....
    });
```

