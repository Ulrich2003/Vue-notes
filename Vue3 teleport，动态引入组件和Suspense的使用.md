# Vue3 teleport，动态引入组件和Suspense的使用

### teleport（传送门）标签
什么是`<teleport to="..."></teleport>`❓
teleport 是一种能够将我们组件的html结构移动到指定位置的技术

**代码模版：**
```html
<teleport to="标签选择器">
	<div>...</div>
</teleport>
```

### 动态引入组件 defineAsyncComponent

✅ 优点：当页面嵌套非常非常多组件的时候，不会因为页面有一个非常小的组件因为网络问题或者其他问题加载不出来，导致整个大组件（页面）没法显示。

```html
<script>
// 动态引入组件
import { defineAsyncComponent } from "vue";
const Person = defineAsyncComponent(() => import("./components/Person.vue"));

export default {
  components: {
    Person,
  },
  setup() {
    return {};
  },
};
</script>
```
### Suspense标签

`<Suspense></Suspense>`需要配合动态引入组件使用，当动态引入的组件因为网络等问题，没办法及时加载出来时，`Suspense`能做到组件占位的作用
**代码模版：**

```html
  <Suspense>
    <template v-slot:default>
      <!-- 这个模版包裹的是动态引入的组件 -->
      <Person></Person>
    </template>
    <template v-slot:fallback>
      <!-- 这个模版包裹的是组件加载不出来时的占位 -->
      稍等，加载中
    </template>
 </Suspense>
```

