﻿# Vue简单介绍Key作用与原理
#### 问题：
- 如果不写key，Vue会做什么？
- 如果写了key，用什么作为key会更加合适？
![在这里插入图片描述](https://img-blog.csdnimg.cn/a6e203753bcf499ea5bab8a3ef1eb615.png)
📢 key是为节点做标识，相当于节点的一个身份证号 🆔


### 如果不写key，Vue会做什么？
如果没有写key，Vue将自动将index索引值作为key。这种没有手动制定key的情况在react下是不允许的🙅‍♂️，所以在Vue里也不推荐这么写。有时会导致一些非常奇怪的问题。
1. 若对数据进行：逆序添加，逆序删除等破坏顺序操作：
会产生没有必要的真实DOM更新，界面效果没问题，但效率低
2. 如果结构中还包含输入类的DOM
会产生错误DOM更新，界面会出现问题❗️
### 如果写了key，用什么作为key会更加合适？
1. 开发中最好使用每条数据的唯一标识作为Key，比如id，手机号等等
2. 如果不存在对数据的逆序添加、逆序删除等破坏顺序的操作，仅用于渲染列表用于展示，使用index作为key是没有问题的

# 原理 💿
面试题： react，vue中的key有什么作用？？（key的内部原理）

虚拟DOM中key的作用：
key是虚拟DOM的对象的标识，当状态中的数据发生变化时，Vue会根据「新数据」生成「新的虚拟DOM」，随后Vue进行「虚拟DOM」与「旧虚拟DOM」的差异比较，比较的规则如下
- 旧虚拟DOM中找到了新虚拟DOM相同的Key：
· 若虚拟DOM中的内容没变，直接使用之前真实DOM
· 若虚拟DOM中的内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOM  
- 旧虚拟DOM中未找到与新虚拟DOM相同的key
· 创建新的真实DOM，随后渲染到页面 📃
