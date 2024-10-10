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









