# Vue对数组元素的监视 

❌ 如果直接用索引下标修改数组中的元素的值，这种方式是不能被Vue监视到的

✅ 但Vue可以监听数组的方法，也就是说，通过方法操纵数组，这种行为是可以被vue监听到的。

常用方法：

- push（）
- pop（）
- shift（）
- unshift（）
- splice（）
- sort（）
- reverse（）

✅ 另外一个修改数组元素的方法，通过Vue.set（）方法修改数组元素。

🌰 例子：修改 user 对象中hobby数组中的第二项的内容

```javascript
Vue.set(vm.user.hobby,1,'骑行');
```

