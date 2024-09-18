Spring创建容器以及子项目

1. 创建容器
   容器就跟 spring boot无关，是一个空的maven容器
   但是现在不能直接创建空容器
   只能先创建 maven java项目，然后删成空的

   在 pom.xml里写上\<packaging>pom\</packaging>
   告诉 idea 这是一个容器，不是项目
   里面的这个依赖就可以删掉了

   ```
   <properties>
       <maven.compiler.source>21</maven.compiler.source>
       <maven.compiler.target>21</maven.compiler.target>
       <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
   </properties>
   ```

   既然是容器，不需要什么源码，所以src也可以删了

2. 然后选择项目结构->新建模块//或者对文件夹右键新建模块
   模块就应该是springboot项目了

   选择 java  maven java21 jar包
   然后下一步，勾选上 Lombok 和 mysql driverr  和 spring data jdbc三个依赖
   完事 子模块就存在了
   但是我们最好在父容器的pom.xml里声明一下 子模块
   加入

   ```
       <modules>
           <module> 模块名称 </module>
       </modules>
   ```

   ![image-20240913090505205](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240913090505205.png)

   模块里的这四个都可以删了

   最好在项目的 pom.xml里加入

   ![image-20240913090938197](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240913090938197.png)

   ```
   <dependency>
               <groupId>org.junit.platform</groupId>
               <artifactId>junit-platform-launcher</artifactId>
               <scope>test</scope>
           </dependency>
   ```

   加快下载速度的

   最后别忘了给模块添加数据源
   MySQL
   主机：就是数据库IP地址

   把模块代码里的 resourse->application什么的删了，自己建一个application.yml的文件
   这个文件里面跟python一样严格缩进

   ```
   spring:
     datasource:
       url: 'jdbc:mysql://120.46.159.231:3306/2022212891?createDatabaseIfNotExist=true'
       username: 2022212891
       password: 2022212891
       hikari:
         maximum-pool-size: 1
     sql:
       init:
         mode: always
   
     logging:
       level:
         sql: debug
         org:
           example: debug
         pattern:
           console: '%-5level %C.%M[%line] - %msg%n'
   里面这样写，注意严格缩进spring必须顶头
   ```

   然后再创建文件 schema.sql 不能写错名字
   然后写入sql语句
   创建表的名字要用 反引号包起来

   ```
   create table if not exists `user`
   (
       id  char(19) not null primary key,
       name varchar(45),
       create_time datetime not null default current_timestamp,
       update_time datetime not null default current_timestamp on update current_timestamp
   );
   
   create table if not exists `address`
   (
       id  char(19) not null primary key,
       name varchar(45),
       user_id char(19),
       create_time datetime not null default current_timestamp,
       update_time datetime not null default current_timestamp on update current_timestamp,
   
       index (user_id)
   );
   ```

3. java-org-example-jdbcexamples下创
   component文件夹放组件
   repository文件夹放持久化接口
    dox文件夹放实体类

   repository里的接口
   比如 UserRepository 要支持增删改查
   有个接口 CrudRepository,让这个接口继承他，然后改一下范型就行
   另外要加上注解 @repository 声明它不是普通接口，他是持久层的组件
   ![image-20240913093450508](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240913093450508.png)

   
   
   
   
   对其创建测试用例
   ![image-20240915210939484](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240915210939484.png)
   
   @SpringBootTest 创建容器 必须加这个注解，说明是Spring测试  不然不能注入
   @Slf4j  打印输出
   
   @Autowired 把这个组件注入进来
   
   
   
   
   
   ![image-20240915223617248](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240915223617248.png)
   要是没有这个控制台，点一下右边的刷新
   
   