# Vue3安装及介绍

1. Nodejs安装
   https://nodejs.org/en/官网下载安装包进行安装
   一路next（中间可以选择安装路径）
   ![image-20240716215859559](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716215859559.png)

   遇到这个点击Add to PATH，可以不用手动添加环境变量
   如果它自动添加变量失败 可以参考https://blog.csdn.net/muzidigbig/article/details/80493880

   安装好后可以打开命令行输入

   node -v 以及 npm -v
   如果显示出来版本号说明安装成功

2. Vue项目创建
   在喜欢的位置新建一个文件夹作为项目的工作空间

   然后在项目内打开命令行（可以直接在文件夹内部打开终端，也就是命令行，也可以win+r 输入cmd  然后 cd 到文件夹位置）

   之后在这个命令行内输入
   npm create vue@latest

   ![image-20240716220421379](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716220421379.png)
   而后让你输入项目名称，那么他会在你打开终端的这个文件夹下面新建一个文件夹作为vue项目
   
   注意 project name 不要输入大写字母！
   
   然后输入前两个绿色的指令，让它自动生成的文件夹安装环境
   
   
   
   这里可以使用 cnpm 代替 npm 因为cnpm是npm的镜像，速度会比较快
   使用npm也行，看个人喜好
   
   
   
   结束后可以运行第三个绿色指令
   ![image-20240716220609984](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716220609984.png)
   复制链接在浏览器打开
   看到
   ![image-20240716220636942](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716220636942.png)
   说明安装成功



## 项目结构介绍

![image-20240716222520414](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716222520414.png)

1.  .vscode  vscode工具的配置文件
   跟项目没关系，删了也行
   今天使用vscode，它会创建一个.vscode
   明天换成idea就会创建一个.idea文件，一样的
   跟使用的工具有关  
2. node_modules
   vue项目的依赖文件夹，里面放的是项目的依赖文件
   npm install命令的目的就是安装这些依赖，如果没有运行这个命令，就没有这个文件夹
3. public
   ![image-20240716223037628](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716223037628.png)
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
   ![image-20240716223312839](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716223312839.png)
   比如项目名称，版本信息···
8. README.md
   注释文件
9. vite.config.js
   vue的配置文件

![image-20240716224415547](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716224415547.png)
create时全部选择否 创建出来的项目是这样的
src里的整个components都可以删掉，因为这是默认的

删完这个后打开app.vue，接着删，删成下面这样
![image-20240716224620214](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716224620214.png)
template和script两者顺序怎么放都行，建议script放下面

### 报错处理

1. 在输入npm create vue@latest后出现以下情况![image-20240716221247213](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240716221247213.png)
    输入以下两串指令
   npm cache clean --force 
   npm config set registry https://registry.npmmirror.com 
   执行上面两行命令后重试

