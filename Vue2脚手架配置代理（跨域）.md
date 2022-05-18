# Vue2脚手架配置代理：

🔗链接：https://cli.vuejs.org/zh/config/#devserver-proxy

### 方法一

在`vue.config.js`中添加以下配置：

```javascript
module.exports = {
  devServer: {
    proxy: 'http://localhost:4000'
  }
}
```

说明：
✅ 优点：配置简单，请求资源时直接发给前端（8080）即可。
⚠️ 缺点：不能配置多个代理，不能灵活的控制请求是否走代理。

🌍 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器（优先匹配前端资源）

### 方法二

```javascript
module.exports = {
  devServer: {
    proxy: {
      '/api1': {
        target: 'http://localhost:5000',
        ws: true,
        changeOrigin: true,
        pathRewrite:{'^/api1',''}
      },
      '/api2': {
        target: 'http://localhost:5001',
        ws: true,
        changeOrigin: true,
        pathRewrite:{'^/api2',''}
      }
    }
  }
}
```

说明：
✅ 优点：可以配置多个代理，且可以灵活的控制请求是否走代理（想走代理加前缀，不想走代理就不加）

⚠️ 缺点：配置略微繁琐，请求资源时必须加前缀。