# Vue3 provide 和 inject的使用

##### `provide()` 和`inject()`的作用
`provide`能向后代组件传递数据，`inject`能在后代组件中接收来自祖先组件传递过来的数据。两个函数联合起来能实现祖孙组件间通信。

![在这里插入图片描述](https://img-blog.csdnimg.cn/7f993d8595724b8caab98faaebb72c03.png)

##### 代码模版：
祖组件中：
```html
<script>
import {provide} from 'vue'
export default {
  setup() {
    provide('msg','这是一条传递给后代的信息')
    return {};
  },
};
</script>
```

后代组件中：

```html
<script>
import { inject } from "vue";

export default {
  setup() {
    let msg = inject('msg')
    return {
      msg
    };
  },
};
</script>
```

