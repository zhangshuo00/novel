# ToDoList 实例
### 1. 输入事项，并保存在状态中
使用 v-model 创建双向数据绑定；
v-on:keyup 监听，并添加按键修饰符 .enter；

```html
<input type="text" v-model="todo" @keyup.enter="addTodo" placeholder="添加待办事项">
```
### 2. 使用 v-for 循环渲染，并通过 v-if 判断是否渲染
```html
<template v-for="(item,idx) in todoList">
	<li :key="idx" v-if="item.done === false">
		<input type="checkbox"><p>{{item.todo}}</p><span>-</span>
	</li>
</template>
```
不允许 v-if 和 v-for 在同一元素内使用，可以在外层包裹 template，v-for 写在template上，v-if 绑定在需要循环的元素上。
### 3. 切换状态和删除
将事件绑定函数写在 methods 属性中
```javascript
changeTodo(idx,done){
	if(done){//标记为已完成事项
		this.todoNum--
		this.todoList[idx].done = true
	}else{//否则标记为未完成
		this.todoNum++
		this.todoList[idx].done = false
	}
},
delTodo(idx,done){
	if(done){
		this.todoNum--
	}
	this.todoList.splice(idx,1)//从待办数组中删除该项
}
```
为待办事项的复选框添加 change 事件，并绑定 changeTodo 函数
```
<input type="checkbox" @change="changeTodo(idx,true)">
```
### 4. 使用 LocalStorage 存储数据，使得刷新页面后数据仍存在
LocalStorage 存储的为字符串格式，getItem 和 setItem 时需要使用JSON.parse 和 stringify 转换格式；
将 getItem、setItem 封装在一个文件中，并导出；
在 todolist.vue 中使用```import * as Utils from ''```引入文件中的多个方法；
或者使用```import {getItem,setItem} from ''```类似es6的解构；
### 5. 数据的初始化及生命周期函数
```
initTodo(){ //初始化函数，从 localstorage中获取数据写入 data中
	var todoArr = Utils.getItem('todoList')
	if(todoArr){
		for(let i=0;i<todoArr.length;i++){
			if(todoArr[i].done === false){
				this.todoNum++
			}
		}
    	this.todoList = todoArr
	}
}
```
在生命周期函数 created() 中调用，修改为 mounted() 函数也可以成功初始化；
**关于生命周期函数还不太清楚，会继续学习**

### 6. 关于路由

**index.js** 中路由的配置

```javascript
import Vue from 'vue'
import Router from 'vue-router'
import Todolist from '@/components/Todolist'// 引入组件
Vue.use(Router)

export default new Router({//创建路由对象
  routes: [//包含多个路由的路径、引入的组件，类似于react中Route的path和component
    {
      path: '/',
      name: 'todolist',
      component: Todolist
    }
  ]
})

```

**App.vue** 中的```<router-view/>```

### 7. 打包

修改 config/index.js 中的 **assetsPublicPath: './'**；

执行 **npm run build** ，打包完成后的文件在 dist文件夹内；

修改 index.html 中引入的 js文件路径，**./static/xxxxxxx**

### 8. 通过 GitHub发布

https://zhangshuo00.github.io/vue-test/one/dist/index.html