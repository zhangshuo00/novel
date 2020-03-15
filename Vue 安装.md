# 创建 Vue项目

### 安装
```
npm install vue-cli -g //全局安装命令行工具
vue init webpack "项目名称" //新建项目
npm install //安装项目依赖
npm run dev //启动项目
```
### 目录结构
![1584256626598](assets/1584256626598.png)
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

### 附
1. 关于命令行参数
```
--save //安装到dependencies生成环境依赖
--global //全局安装
--save-dev //安装到devDependencies开发环境依赖
--save-optional //安装到optionalDependencies可选环境依赖
```
