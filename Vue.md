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

