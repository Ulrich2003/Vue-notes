### Vue中的ref属性

1. ref属性被用来给元素或子组件注册引用信息（id的替代者）

2. 应用在html标签上获取的是真实DOM元素，应用在组件标签上是组件实例对象（vc）

⭕️ 使用方式：

```html
<h1 ref="xxx">...</h1>
<School ref="xxx"></School>
```

⭕️ 如何获取ref：

`this.$refs.xxx`