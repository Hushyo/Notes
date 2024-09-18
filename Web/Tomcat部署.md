# Tomcat部署

Tomcat部署

![屏幕截图 2024-06-12 200829](E:/%E5%9B%BE%E7%89%87/Webimg/Tomcat/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-06-12%20200829.png)

 /web代表项目部署在根服务器的地址, 如果只写一个/ 则代表项目部署在根目录

那么此时 Tomcat启动时，访问的地址为
![屏幕截图 2024-06-12 201104](E:/%E5%9B%BE%E7%89%87/Webimg/Tomcat/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-06-12%20201104.png)

http://localhost:8080/是本地的根服务器，项目部署在此服务器上
该项目的路径为 http://localhost:8080/Web/
想访问项目里的资源需要在这个路径下添加资源的路径
比如
![image-20240612202805581](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612202805581.png)

webapp就代表这个项目，想访问webapp下的main.html
就要在启动服务后的项目路径后加上 main.html
完整写出来就是
http://localhost:8080/Web/main.html



服务器可以部署多个项目，用路径区分

这种部署是热部署
因为这是开发阶段，需要多次修改，修改完可能要编译，部署。
但Tomcat默认每次修改都重启服务器，浪费资源且没必要，所以改下面这个
![image-20240612201435900](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612201435900.png)

把默认的 `重启服务器` 改为 `更新类和资源` 不需要重启服务器

下面这个也改，为什么改？作用是什么？
当你还没写完idea时切出去了没保存，他会自动更新保存 

或者改完idea代码，想切到浏览器里看看效果。
它就会自动完成部署,浏览器就会更新。

![image-20240612201740488](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612201740488.png)

注意 这是 更新类和资源
什么意思呢？已经存在的类和资源 才叫更新
更新对存在的东西才有效

如果是部署后，在项目里新建了一个类或资源。这部分是不会更新到服务器上的
因为他们是新的，不是更新，这种就需要重新部署到服务器上
如果重启还不好使，那么就在停止后  maven->生命周期->clean
还不好使？那就是这个新加的东西有问题了





代表Tomcat服务器启动时，占用本地的哪个端口。默认是8080端口

![image-20240612201850700](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612201850700.png)

在IDEA里
![image-20240612202103048](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612202103048.png)
这儿可以随时部署新的项目



运行用Debug模式 （那个瓢虫）



Tomcat控制台输出很多乱码
![image-20240612203622350](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612203622350.png)

控制台的东西是Tomcat发出的，不是idea
1.改idea的属性

![屏幕截图 2024-06-12 203748](E:/%E5%9B%BE%E7%89%87/Webimg/Tomcat/%E5%B1%8F%E5%B9%95%E6%88%AA%E5%9B%BE%202024-06-12%20203748.png)

在这儿加上一句
-Dfile.encoding=UTF-8
然后重启idea

2.Tomcat的VM参数

![image-20240612204121534](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612204121534.png)

在这儿也加上

乱码问题解决