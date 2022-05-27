# Vue3自定义hook函数的使用，代码模版
什么是hook❓**本质就是一个函数**

类似于vue2的`mixin`

自定义hook的优势：复用代码，让setup中的逻辑更清楚易懂![在这里插入图片描述](https://img-blog.csdnimg.cn/1c46c145ef3b4b71b5aa406df4981871.png)

`hook`的本质就是一个函数，所以在`.js文件`中写一个默认暴露的函数，并且返回一些`setup()`里面会用到的关键数据

### 编写`hook`函数

```javascript
import { onBeforeUnmount, onMounted, reactive } from "vue";

export default function(){
    let point = reactive({
        x: 0,
        y: 0,
        ...
      });
  
      function savePoint(event) {
        ....
      }
  
      onMounted(() => {
        ....
      });
  
      onBeforeUnmount(() => {
        ....
      });

      return point
}
```

### 在`setup()`里面使用`hook`函数

```html
<script>
// 引入hook
import usePoint from "../hook/userPoint";
export default {
  setup() {
  	// 使用hook
    let point = usePoint();
    return {
      point
    };
  },
};
</script>

```

