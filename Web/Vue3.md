vue官方文档https://cn.vuejs.org/guide/essentials/application.html

# Vue3安装

## 安装前置

Nodejs安装
https://nodejs.org/en/官网下载安装包进行安装
一路next（中间可以选择安装路径）
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716215859559.png" alt="image-20240716215859559" style="zoom:67%;" /> 

遇到这个点击Add to PATH，可以不用手动添加环境变量
如果它自动添加变量失败 可以参考https://blog.csdn.net/muzidigbig/article/details/80493880
安装好后可以打开终端(Win+R+cmd)输入node -v 以及 npm -v
如果显示出来版本号说明安装成功



Node.js是一个基于V8引擎的JavaScript运行环境， 提供了一些功能性的API，例如文件操作API、网络 通信API等。



安装完Node.js后就有了npm和vite，都包含在内的
npm也可以用来安装yarn



npm和yarn是常见的包管理工具
“包”可以 理解为将一系列模块化的代码打 包起来，形成一个包，以便于使用。
项目中所用到的包称为项目的依赖（dependency）

vscode里面不能用yarn命令，所以用npm创建项目

## 项目创建

Vue项目创建
在喜欢的位置新建一个文件夹作为项目的工作空间

然后在项目内打开命令行
可以直接在文件夹内部打开终端，也就是命令行
也可以win+r 输入cmd  然后 cd 到该文件夹内部
之后在这个命令行内输入
**`npm create vue@latest`**

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716220421379.png" alt="image-20240716220421379" style="zoom:80%;" /> 
而后让你输入项目名称，那么他会在你打开终端的这个文件夹下面新建一个文件夹作为vue项目
注意 project name 不要输入大写字母！
然后输入前两个绿色的指令，让它自动生成的文件夹安装环境

cd vuetest 这里是进入刚才创建的文件夹内部
npm install 这是在这个文件夹内安装npm

这里可以使用 cnpm 代替 npm 因为cnpm是npm的镜像，速度会比较快
使用npm也行，看个人喜好

结束后可以运行第三个绿色指令运行项目
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716220609984.png" alt="image-20240716220609984" style="zoom:67%;" /> 
复制链接在浏览器打开
看到
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716220636942.png" alt="image-20240716220636942" style="zoom:50%;" /> 
说明安装成功





方法二 vite

目前还是不要用这个了，这个创建完怎么没有App.vue?
所以用vue@latest



输入 
`npm create vite@latest`
然后输入名字，选择`JavaScript`就直接成功了
下一步，`cd 项目名`，进入项目
输入 `npm install `安装包管理工具
之后输入` npm run dev `启动服务，它会给一个链接 打开是 
<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240930184632964.png" alt="image-20240930184632964" style="zoom:33%;" /> 



## 项目结构介绍

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716222520414.png" alt="image-20240716222520414" style="zoom: 50%;" /> 

1.  .vscode  vscode工具的配置文件
   跟项目没关系，删了也行
   今天使用vscode，它会创建一个.vscode
   明天换成idea就会创建一个.idea文件，一样的
   跟使用的工具有关  
2. node_modules
   vue项目的依赖文件夹，里面放的是项目的依赖文件
   npm install命令的目的就是安装这些依赖，如果没有运行这个命令，就没有这个文件夹
3. public
   <img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716223037628.png" alt="image-20240716223037628" style="zoom:50%;" /> 
   ![image-20240716223046126](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716223046126.png)
   里面放的图片是浏览器页面标签左上角的图标
4. scr
   源码文件夹，代码写在这里
5. .gitignore
   git的忽略文件，团队之间需要用到的
6. index.html
   入口html文件
   不要丢也不要改，所有的代码都会引入到这个文件里运行
7. package.json
   描述项目信息的
   <img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716223312839.png" alt="image-20240716223312839" style="zoom: 50%;" />  
   比如项目名称，版本信息···
8. README.md
   注释文件
9. vite.config.js
   vue的配置文件

![image-20240716224415547](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716224415547.png)
create时全部选择否 创建出来的项目是这样的
src里的整个components都可以删掉，因为这是默认的

删完这个后打开app.vue，接着删，删成下面这样
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716224620214.png" alt="image-20240716224620214" style="zoom:80%;" /> 
template和script两者顺序怎么放都行

## 报错处理

1. 在输入npm create vue@latest后出现以下情况<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716221247213.png" alt="image-20240716221247213" style="zoom:50%;" /> 
    输入以下两串指令
   npm cache clean --force 
   npm config set registry https://registry.npmmirror.com 
   执行上面两行命令后重试



# Vue3介绍

Vue 是基于MVVM模式的框架

MVVM: Model View ViewModel
Model 数据部分  
View 视图部分  我们能够看到的
ViewModel 用于连接视图与数据模型，负责监听View或者Model的改变

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240930181858884.png" alt="image-20240930181858884" style="zoom: 50%;" /> 

DOM listener监听事件
Data Binding 数据绑定

View和Model不能直接通信，达到解耦效果



VSCODE可以同时运行多个终端的项目
只需要右键项目，选择在集成终端中打开
然后 npm install  npm run dev 就行了





# Vue基础

1. index.html是入口，非常重要，但是里面基本不写东西
   用link引入其他东西，或者把组件挂在里面的元素上

   <img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20241011135251388.png" alt="image-20241011135251388" style="zoom:67%;" /> 

2. 项目结构里 路径 src 下可能有一个 style.css  可以删掉
   比年项目创建自带的样式代码影响项目效果

3. 



## API

Vue 的组件可以按两种不同的风格书写：**选项式 API** 和**组合式 API**
目前更推荐组合式API



## 单文件组件

每个 .vue 文件都是一个单文件组件
每个单文件组件都由  模板、样式 和 逻辑 三部分构成

1. 模板
   用于搭建当前组件的DOM结构
   代码在 \<template> 标签中

   把\<template>标签当作body标签用就挺好的

2. 样式
   组件中的CSS样式
   代码在 \<style>标签中

3. 逻辑
   指的是通过JS代码处理组件的数据与业务
   代码在 \<script> 标签中

App.vue是全局组件
把所有东西都写在App.vue里也不是不行，只是后期维护起来可能不太方便

所以我们把组件分块写，放在 components 包里，由App.vue引入使用
然后把 App.vue 通过main.js 挂在 index.html 里的元素上



组件如何使用
main.js中

```
import './assets/main.css'
这个是样式，可以删掉

import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')
```

- import { createApp } from 'vue'
  这个是从 vue 中引入方法 createApp
  导入方法用{ }包括方法名即可，不同方法之间用逗号隔开

- import App from './App.vue'
  这个是引入 App.vue 这个组件   起别名为 App
  命名随意的，引入和命名名字不一样也没问题

   ./ 代表本文件所在的目录

- createApp(App).mount('#app')
  调用方法 createApp(App) 传入 App.vue 组件作为参数
  效果是创建一个应用实例（App）
  然后调用 app.mount方法
  app.mount("#app") 这个方法把刚才创建的应用挂到 id为app 的元素上，然后渲染出来
  这个就是组件的运行过程



每个 Vue 应用都是通过 [`createApp`](https://cn.vuejs.org/api/application.html#createapp) 函数创建一个新的 **应用实例** app

function createApp(rootComponent: Component, rootProps?: object): App
第一个参数是根组件。第二个参数可选，它是要传递给根组件的 props
根组件可以是内联的，也可以是外部导入的 如 improt App from './App.vue'

app.mount( )将应用实例挂载在一个容器元素中
参数可以是一个实际的 DOM 元素或一个 CSS 选择器 (使用第一个匹配到的元素)
对于每个应用实例，`mount()` 仅能调用一次
但是我们可以创建多个应用实例多次调用啊

## 数据绑定

Vue通过数据绑定是西安了数据与页面分离
实现了数据驱动页面的效果，也就是 把页面的数据分离出来放到组建的 script 标签中
通过程序操作数据，并且数据改变时，页面会自动发生改变，拒绝硬编码！

数据绑定分为 定义数据 和 输出数据
定义数据发生在 scrpit 标签中
输出数据 使用 Mustache语法（双大括号法）把数据输出到页面

代码写作 {{数据名}}  在页面里渲染出来数据名对应的值

### 定义数据

语法格式如下

```
<script>
export default{
调用方法 setup(),以对象形式返回数据，一个对象的不同元素用逗号分隔
  setup(){
    return {
      数据名：数据值,
      数据名：数据值,
      ...
    }
  }
  
}
</script>
```

  为了让代码更简洁，Vue3提供了 setup语法糖 
使用它可以更方便开发

```
<script setup>
var/const/let 数据名 = 数据值
</script>
```

### 输出数据

Mustache语法，这种语法相当于在 template 中放入了占位符
**`{{ 数据名 }}`**

这种语法内部也可以直接写一个表达式，页面会渲染表达式的值

```
{{"hello"}}->hello
{{number+1}}
{{obj.name}}
{{ok?yes:no}}
{{'<div></div>'}}-><div></div>
```



例子

```
demo.vue:
<template>{{ message }}</template>
<script setup>var message = "数据输出";</script>

main.js:
import { createApp } from 'vue'
import App from './components/demo.vue'
				可以通过切换这个👆测试不同组件
createApp(App).mount('#app')
页面渲染：数据输出
```

## 响应式数据绑定

想要实现页面中数据的更新，需要进行响应式数据绑定，也就是将数据定义成响应式数据
响应式数据发生变化时，页面会重新渲染一遍，有四种函数可以定义响应式数据

1. ref( )
   用于将数据转化成响应式数据，参数为数据，返回值为转换完成的响应式数据

   语法格式：响应式数据 = ref（数据）
   如果需要更改数据的值
   响应式数据.value = 新值

   ```
   <template>{{ message }}</template>
   
   <script setup>
   
   import {ref} from 'vue' //引入方法才能用
   
   var message = ref("数据输出");
   setTimeout(()=>{
       message.value='锲而不舍'
   },2000)
   
   </script>
   ```

   页面刚开始是 数据输出 过两秒变成 锲而不舍二

2. reactive( )
   用于创建一个响应式对象或者数组，将普通的对象或数组作为参数传进去，返回响应式的
   响应式对象或数组 = reactive(普通对象或数组)
   改值？
   对象.属性 =新值

   ```
   <template> {{ obj }} </template> //记得数据名要对
   
   <script setup>
   
   import {reactive} from 'vue' //记得引入方法
   
   var obj = reactive({name:"pang",id:1});
   setTimeout(()=>{
       obj.name="Hush"
   },2000)
   
   </script>
   ```

3. toRef( )
   将响应式对象中的单个属性转换为响应式数据，返回转换完成的响应式数据，而不是对象
   响应式数据 = toRef(响应式对象，"属性名")

   ```
   <template>
       <div>obj.name的值:{{ obj.name }}</div>
       <div>message的值: {{ message }}</div>
   </template>
   <script setup>
   import { reactive,toRef } from 'vue';
   var obj = reactive({name:"pang",id:1});
   var message = toRef(obj,"name");
   setTimeout(()=>{
       message.value="Hush";
   },3000);
   
   </script>
   ```

   使用 `toRef` 创建的响应式引用和原始对象中的属性不是同一个，但它们是相互关联的。
   这意味着，当你修改响应式引用的值时，原始对象中的对应属性也会被更新，反之亦然

4. toRefs( )
   将响应式对象中的所有属性转换为响应式数据
   所有属性组成的对象 = toRefs(响应式对象)
   返回一个由响应式数据构成的对象
   提问，响应式数据如何改值？数据.value!

   ```
   <template>
       <div>obj的值:{{ obj }}</div>
       <div>obj2的值: {{ obj2 }}</div>
   </template>
   
   <script setup>
   import { reactive,toRefs } from 'vue';
   var obj = reactive({name:"pang",id:1});
   var obj2 = toRefs(obj);
   
   setTimeout(()=>{
   
       obj2.name="Hush";
       obj2.id="666"
   	写成上面这个是不会改的！
       obj2.name.value="Hush";
       obj2.id.value="666"
       
   },3000);
   
   </script>
   ```

响应式数据与非响应式数据的区别？看个例子

```
<template>
    <div>obj的值:{{ obj }}</div>
    <div>obj2的值: {{ obj2 }}</div>
    <div>obj3:{{ obj3 }}</div>
</template>
<script setup>
import { reactive,toRefs } from 'vue';
var obj = reactive({name:"pang",id:1});
var obj2 = toRefs(obj);
var obj3 = {name:"yu"};

setTimeout(()=>{
    obj2.name.value="Hush";
    obj2.id.value="666"
},1000);
setTimeout(()=>{
    obj3.name="hao"
},2000)

</script>
```

页面一秒后，响应式数据改变，页面重新渲染
但是两秒后，非响应式数据改变，页面不变，obj3显示的内容仍然是初始值 yu 而不是 hao
