# Vue 路由

**使用 Vue + Vue Router 创建单页应用**
1. 定义路由组件

2. 定义路由**./router/index.js**，配置路径，并将组件映射到路由上，然后创建router实例
```javascript
Vue.use(Router)

export default new Router({
  routes: [
    {path: '/',name: 'Home',component: Home},
    {path:'/pins',name:'Pins',component:Pins},
    {path:'/topics',name:'Topics',component:Topics},
    {path:'/books',name:'Books',component:Books},
    {path:'/events',name:'Events',component:Events}
  ],
  mode:'history'
})
```
3. 创建和挂载跟实例
```javascript
import Vue from 'vue'
import App from './App'
import router from './router'

Vue.config.productionTip = false

new Vue({
  el: '#app',
  router,
  components: { App },
  template: '<App/>'
})
```
**Nav.vue**
```javascript
<!-- 使用 router-link 组件进行组件映射到路由 -->
<!-- 通过 to属性进行链接 -->
<router-link to="/" exact>首页</router-link>
<router-link to="/pins" exact>沸点</router-link>
<router-link to="/topics" exact>话题</router-link>
<router-link to="/books" exact>小册</router-link>
<router-link to="/events" exact>活动</router-link>
```
**App.vue**
```
<template>
  <div id="app">
    <pagenav></pagenav>
    <router-view></router-view>
  </div>
</template>
```
**router-link**类似于react中的`<Link>`组件，通过 to属性指定到目标路由，添加`exact`属性进行精准匹配路径；
**router-view**可以使用多个，用来展示多个视图，而不是嵌套展示。
```javascript
<router-view class="view one"></router-view>
<router-view class="view two" name="a"></router-view>
<router-view class="view three" name="b"></router-view>

const router = new VueRouter({
  routes: [
    {
      path: '/',
      components: {
        default: Foo,
        a: Bar,
        b: Baz
      }
    }
  ]
})
```
#### 动态路由匹配

