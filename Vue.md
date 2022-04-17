解决部分低版本安卓浏览器不支持Promise（ES 6新特性）的问题（还出现白屏情况的打包编译即可解决）。安装babel-polyfill依赖包（执行npm install babel-polyfill--save命令），在Vue项目的main.js中编写import 'babel-polyfill'引用即可。



解决移动端某些版本浏览器单击事件延时触发的问题。安装fastclick依赖包（执行npm install fastclick--save-dev命令），在Vue项目的main.js中将fastclick绑定到body即可。

执行命令如下

```
import fastClick from 'fastclick'
fastClick.attach(document.body)
```







滚动操作
@wheel.passive
常用按键别名：
回车：enter
删除：delete
退出：esc
空格：space
换行：tab （特殊，配合keydown使用）
上：up
下：down
左：left
右：right


watch 
handler：数值改变时执行
deep： true时监听属性，false
immediate: 初始化执行 

-   `.stop` - 阻止冒泡
-   `.prevent` - 阻止默认事件
-   `.capture` - 阻止捕获
-   `.self` - 只监听触发该元素的事件
-   `.once` - 只触发一次
-   `.left` - 左键事件
-   `.right` - 右键事件
-   `.middle` - 中间滚轮事件



## es6

组件暴露：

分别暴露：export const name = Vue.extend(){}

默认：export default name 

统一：export{name1,...}



查看webpack配置：

vue inspect > output.js



全局事件总线

```
beforeCreate(){
	Vue.prototype.$bus = this
}

mounted(){
	this.$bus.$on('hello',(data)=>{
    	console.log('school组件接收到了',data)
    })
},

methods:{
	send(){
    	this.$bus.$emit('hello',this.name)
	}
}
```



绑定事件

this.$emit绑定一个事件

this.$off('name ') 解绑一个事件

this.$of(['name1','name2']) 解绑name1,name2

this.$off()解绑所有事件





代理服务器

```
const options = {
  target: 'http://www.example.org', // target host
  changeOrigin: true, // needed for virtual hosted sites
  ws: true, // proxy websockets
  pathRewrite: { //重写地址
    '^/api/old-path': '/api/new-path', // rewrite path
    '^/api/remove/path': '/path', // remove base path
  },
  router: { //路由
    // when request.headers.host == 'dev.localhost:3000',
    // override target 'http://www.example.org' to 'http://localhost:8000'
    'dev.localhost:3000': 'http://localhost:8000',
  },
};
```



vue的请求发送

axios

vue-resourse( 插件 )：Vue.use(vueResource)

axios -> this.$http 

