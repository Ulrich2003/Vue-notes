### Vue2 / Vue3响应式实现方案原理模拟，只是简单的模拟

｜｜来源：尚硅谷前端vue视频，它家的视频巨好

### 「模仿」Vue2响应式实现方案

⭕️ 原理：使用defineProperty()

```javascript
let person = {
  name:'ulrich'
}
let p = {}
Object.defineProperty(p,'name',{
  configurable: true,
  get(){
    return person.name
  },
  set(value){
    console.log('有人修改了p身上的属性，我发现了，我要去修改页面')
    person.name = value
  }
})
```

### 「模仿」Vue3响应式实现方案

⭕️ 原理：proxy

```javascript
let person = {
  name:'ulrich'
}
let p = new Proxy(person,{
  get(target,propName){
    return Reflect.get(target,propName)
  },
  set(target,propName,value){
    console.log('有人修改了p身上的属性，我发现了，我要去修改页面')
    Reflect.set(target,propName,value)
  },
  deleteProperty(target,propName){
    console.log('有人删除了p身上的属性，我发现了，我要去修改页面')
    return Reflect.deleteProperty(target,propName)
  }
})
```

