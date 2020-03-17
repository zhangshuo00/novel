# 创建 Vue项目

### 安装
```
npm install vue-cli -g //全局安装命令行工具
vue init webpack "项目名称" //新建项目
npm install //安装项目依赖
npm run dev //启动项目
```
### 目录结构
```
build //webpack相关
config //配置目录
src-
  |--assets //图片文件
  |--components //组件
  |--App.vue //项目入口文件
  |--main.js //核心文件
static //静态资源目录
```
### 语法
```javascript
var data = {text:'hello',name:'zhangsan'} //定义属性 
var vm = new Vue({
	el:'#app', //DOM元素中的id
	data:data,
	methods:{ //定义函数
		details:function(){
			return this.text + 'world'
		}
	}
})
// (vm.text === data.text) true 引用相同的对象
```
将DOM绑定在vue实例，并且使用模版将数据渲染到DOM
#### 插值
```
1. <p> {{msg}}</p>//可以在data中定义msg的内容
2. <div v-html="msg"></div>//使用v-html指令可以插入html代码，msg定义为'<h1>hello</h1>'
3. <div v-bind:class="{'class1':use}">
 		通过use的值，判断是否使用class1
 		use的值可在data中定义
	</div>
4. {{true?'hello':'world'}}//可以在{{}}中插入表达式
```
#### 指令
**v-bind**给元素的属性绑定一个值
```javascript
<a v-bind:href="url">地址</a>
<a :href="url">地址</a> //缩写
```
**v-model**在 input、select、checkbox、textarea等表单控件元素上实现双向数据绑定，根据表单上的值，自动更新绑定元素内的值。
```
<div id="app">
	<p>{{msg}}</p>
	<input v-model="msg"/>
</div>
<script>
new Vue({
	el:'#app',
	data:{
		msg:'hello,world!'
	}
})
</script>
```
**v-on**监听事件
```
<button v-on:click="fetchData"/>
```
**v-if** 
**v-else-if**
**v-else**
条件渲染，如果在初始值为false，是不会渲染的；直到条件为true时，才会渲染

```
<div id="app">
	<p v-if="seen === 'a'">hello,world</p>
	<p v-else-if="seen === 'b'">hello,zhangsan</p>
	<p v-else>hello,vue</p>
</div>
<script>
new Vue({
	el:'#app',
	data:{
		seen:'a'
	}
})
</script>
```
**v-for**通过循环渲染元素
```
<div id="app">
	<ul>
		<li v-for="(item,idx) in items" v-bind:key="idx">
			{{item}}
		</li>
	</ul>
</div>
<script>
new Vue({
	el:'#app',
	data:{
		items:['zhangsan','lisi','wangwu']
	}
})
</script>
```
也可以提供第二个参数为键名：
```
<li v-for="(value,key,idx) in user" :key="idx">
{{key}}:{{value}}
</li>
data:{
	user:{
      name:'zhangsan',
      id:'1111',
      email:'11111'
    }
}
```
增加第三个参数为索引
```
<li v-for="(value,key,idx) in user" :key="idx">
{{idx}}:{{key}}:{{value}}
</li>
```
**v-show**是否显示元素，相当于 display:none；区别于v-if，无论初始条件是什么，都会进行渲染。

### 附
1. 关于命令行参数
```
--save //安装到dependencies生成环境依赖
--global //全局安装
--save-dev //安装到devDependencies开发环境依赖
--save-optional //安装到optionalDependencies可选环境依赖
```
