图片在GitHub，不用魔法可能不显示

# SpringBoot

## Microservices

<font color=229453>传统单体架构下，当需求不断变更时，应用将变得臃肿，更新维护将变得更加困难</font>
<font color=green>资源无法隔离，各功能模块依赖相同的数据库/内存/CPU等资源，单一功能缺陷会造成整个应用瓶颈</font>
<font color=green>无法实现灵活高效的扩展，只能平行扩展整个应用</font>

因此引入了微服务架构
服务即为独立，开发/测试/部署/运行/更新/维护的，通过对外暴露接口而隐藏实现的服务

- 每个服务可由不用程序语言编写
- 服务之间通过成熟的HTTP等协议通信
- 每个服务可以独立快速完成开发/测试
- 每个服务以最小规模独立运行部署，便于后期维护以及弹性扩展为服务集群

而且微服务可以单独弹性部署扩充，比如打车，搜索车辆的用户比实际付款的人多得多，因此可以多为打车服务部署服务器

## SpringBoot

### Introduction

<font color = green>以前基于SpringMVC+Spring+JPA的开发，需创建JPA持久化单元配置，hibernate实现配置，spring容器配置，web.xml启动SpringMVC及Spring容器配置，日志配置等。创建spring项目过于复杂</font>
现在引入了Spring，Spring提供springboot框架，减少了开发配置的困难，使创建基于spring的独立的产品化的程序变得简单

- 约定大于配置，极大的减少了配置

- 提供了各种开箱即用的功能

- 集成了可直接运行的嵌入式web服务器，便于部署

- 是创建微服务项目的理想实现

此处省略SpringBoot项目的创建



### Slf4J


<font color=green>使用Log4j2等日志框架，会使项目与具体的日志框架耦合；所有库都需日志输出，项目可能因此导入多个不同日志框架</font>
Slf4j(Simple logging facade for Java)
提供了一套日志API接口，使所有实现了其接口的日志框架可以自由切换。Log4j2等框架均实现了Slf4j接口

- 支持控制台/文件(log/html/json等)/数据库等输出
- 支持定义输出样式，文件分割模式等
- 支持占位符输出，不必if enabled判断
- 支持直接输出异常栈信息

日志分为许多等级，可以调整等级来控制日志输出的内容，每个级别都有对应的日志方法

| 等级  | 作用                                                         |
| :---: | :----------------------------------------------------------- |
|  off  | 关闭日志记录                                                 |
| fatal | 无法修复，可能导致系统终止的严重错误信息                     |
| error | 无法修复，但系统依然可以运行的错误信息                       |
| warn  | 未影响运行，但存在潜在的危害的警告信息                       |
| info  | 系统当前运行状态运行过程信息，例如启动，关闭等，粗粒度       |
| debug | 调试输出信息，例如编写代码时在所有逻辑分支的调试输出，细粒度 |
| trace | 追踪信息                                                     |
|  all  | 打开所有日志                                                 |

springboot框架已包含slf4j接口及Logback实现依赖，无需显式声明引入，即无需声明依赖

我们可以在application.yml里声明日志配置

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240918172217331.png" alt="image-20240918172217331" style="zoom:67%;" /> 

logging:level，声明不同包的路径日志级别，root为最顶层节点，声明root全局warn以上级别输出
下面的那个则声明 com.example下的日志输出等级为debug，输出日志时只能输出debug及更高级的日志

在application.yml里 logging用来配置日志系统，可以按上面那样写
也可以一项项单独写 比如 logging.level.root: warn , logging.pattern.console: ··· 



### Lombok

Lombok框架，通过增加一些`处理程序`使java程序变得更简洁
Lombok在编译时添加生成代码，而非基于运行时反射，因此执行效率高。
Idea默认已包含lombok插件，不需要额外引入

|        注解         |                             作用                             |
| :-----------------: | :----------------------------------------------------------: |
|       @Slf4j        | 自动为类生成一个日志对象，从而避免了在每个类中手动编写日志对象的代码 |
|   @Getter/@Setter   |                     编译时添加Get/Setter                     |
|        @Data        |        包含@Getter/Setter/@ToString/@EqualAndHashcode        |
| @NoArgsConstructor  |                       添加无参构造函数                       |
| @AllArgsConstructor |                     添加各种有参构造函数                     |
|      @Builder       | 添加Builder模式<br />但是必须同时添加@NoArgsConstructor/@AllArgsConstructor |
|                     |                                                              |

## JDBC

JDBC优点不写，缺点 SQL语句以硬编码形式写于代码中，不利于维护移植，原生JDBC同步阻塞

ORM 对象关系映射
一种为了解决面向对象与关系数据库不匹配现象的技术
无需关心底层数据库，只需要面向对象实现细节（不管是用哪种数据库都可以）

### **Spring-data-jdbc**

Spring-data是 Spring的子项目，看名字就知道，而 jdbc又是Spring-data的一个子项目。
提供了统一的编程模型/接口，简化了数据访问层的开发工作
包括通用的CRUD操作/查询方法/事物管理和数据访问抽象层等

idea里添加database视图并添加数据库可以让项目支持对数据源操作的自动提示
具体怎么添加数据源，看之前的笔记
如果没有自动提示，在编写SQL代码的时候按alt+enter打开语法提示 然后推荐选择MySQL语法



**数据库初始化**

基于SpringBoot自动配置策略，引入持久化框架时，自动读取配置中的数据源配置
如果没有配置数据源则抛出异常无法启动				配置中添加自动创建数据库参数
在Application中 spring下声明 sql.init.mode: always 
每次启动spring时就会加载一下 resources下的schema.sql文件来初始化数据库
不声明则不会自动执行sql脚本

为什么加载这个？因为这是默认配置，如果你的sql文件不叫这个，那就加载不动了，所以要按规范命名配置文件

sql文件下，放的是初始化数据库的代码
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20241003160243030.png" alt="image-20241003160243030" style="zoom:50%;" /> 

用反引号 `` 包括表名，防止表名与关键字冲突

最好用 if not exists 因为每次启动都要执行一遍脚本，但我们只需要在第一次执行的时候创建表
如果表存在就不创建了
但是这样也存在一些问题，我们在旧表里添加新字段，但是执行脚本时由于旧表存在，并不会更新旧表
脚本进支持判断是否需要创建数据表，如果数据表存在而想改变/添加字段时，只能我们手动更改数据表

对于表中的外键，我们不直接声明外键，而是在外键上建立索引
因为互联网经常跨表，跨库，外键约束不了，于是干脆不约束了





### 开发规范

OR Mapping

一个类映射为一张数据表
类的一个属性映射为数据表中的一个字段（键）
类的一个对象映射为数据表中的一条记录（一个元组）

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20241003154830460.png" alt="image-20241003154830460" style="zoom:67%;" /> 

映射发生在哪里下面一点一点揭晓，现在只需要映射规则，只要名字对，不管什么类型都能映射进去





**DO**
与数据库表结构一一对应的类
一个DO就可以理解为一张Mysql里的表，不过这个表是实体的一个Java类，一个DO的对象就表示mysql里的一条数据。
但是DO类的包不允许名字是do，所以我们用dox作为包名来放置DO类
课程中的各个实体entity类其实就是DO类



**DAO**



**DTO**

数据传输对象，通过Service层按需求组织DO数据封装到DTO对象
DTO 简单理解就是接收前端传递过来的数据的，
比如前端给你传递一个POST请求，你想用对象进行接收，此时我们就会使用DTO对象来接收。

**VO**

显示层对象，向视图传输的对象
VO简单来说，就是我们返回给前端数据用的对象就是VO
比如你从数据库查了一些表的部分信息，封装之后，要返回给前端，此时你就你可以用一个VO来进行封装，返回给前端。



所有用于封装数据的，仅包含属性不包含处理逻辑（业务）的类统称为POJO类（贫血模式）
POJO类必须包含

- 无参构造函数。各种框架使用反射构造对象
- 所有属性不声明初始值。在操作时显示赋值，避免忘记初始值
- 属性必须声明为 private或者protected
- 基本数据类型属性 声明为引用属性 int->Integer 避免默认值 默认是0跟不存在是不同的意义
- 严格按规约声明 getter/setter方法
- 声明为非 final 类
- 多使用组合 少使用继承

**映射规则**
数据库中 所有库/表/字段名全部小写，单词间用下划线连接
java中 驼峰式命名
Spring自动按照约定进行映射，所以自己写的时候要按规矩写

user_name->userName
create_time->createTime
就这么映射，反向也是这个规则



### 实例

来看一个DO类吧

```
@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class User {
    @Id
    @CreatedBy
    private String id;
    private String name;
    @ReadOnlyProperty
    private LocalDateTime createTime;
    @ReadOnlyProperty
    private LocalDateTime updateTime;
}
```

主要关心类里面的注解
注解可以叠加，但是只作用于下面第一个出现的属性
像是@Id,@CreateBy它俩只作用于第一个出现的 id属性

**@Id** 声明属性为主键
**@CreateBy** 声明属性为审计字段，一般用于填充用户信息，这个过程不需要我们来完成，但我们需要告诉jdbc从哪儿获得用户信息 
**@ReadOnlyProperty** 声明属性为只读属性，也就是我们读数据的时候考虑这个属性，在进行其他操作时比如持久化（如保存）时会忽略这个属性

**雪花算法**

```
@Configuration
@EnableJdbcAuditing
public class SnowflakeGenerator {
    @Bean
    AuditorAware<String> auditorAware() {
        Snowflake s = new Snowflake();
        return () -> Optional.of(String.valueOf(s.nextId()));
    }
```

**@EnableJdbcAuditing** 注解用于启用 Spring Data JDBC 的审计功能
当启用后，它会自动填充使用 `@CreatedBy`、`@CreatedDate`、`@LastModifiedBy` 和 `@LastModifiedDate` 注解的字段

**@Configuration**注解标记一个类作为配置源，替代传统的 XML 配置文件

 **@Bean**注解 它用于指示方法应该返回一个对象，该对象应该被注册为 Spring 应用上下文中的 Bean，这样 Spring 才能识别并使用它，给上文的@CreateBy注解的属性完成自动填充



**为什么数据库中id要用19位字符接收？为什么不用整形？**
在MySQL中，bigint/char类型主键没有性能差异，但是在前端中String可以避免JS无法处理19位整数的精度丢失问题
因此使用19位字符作为主键id



### CrudRepository

**CrudRepository<T,ID>** 接口提供了针对DO类的基本CRUD操作（create read update delete)

`CrudRepository`接口提供了一组基础的CRUD操作，包括保存、删除、查询等方法。

T操作的DO类型，ID主键类型

T save(S entity) 方法 默认保存全部属性值，值为null时也会保存到数据库，因此可能覆盖数据库设置的默认值
如果数据库中存在同样的对象但是属性值不同，新的属性值会覆盖旧的属性值，也就是完成了update操作

还有其他方法，先不写



使用：
创建一个名为 repository的包，专门放置各种组件
如对User处理的组件就创建一个名为 UserRepository 的接口，这个接口继承以上这个CRUD接口
`CrudRepository` 提供了一组标准的 CRUD 操作，而 `UserRepository` 接口通过继承它，自动获得了这些操作的实现

**@Repository注解**
Spring 应用启动时，它会扫描带有 `@Repository` 注解的类，并自动将这些类注册为 Spring 应用上下文中的 Bean
Spring 会管理这些类的生命周期，并且可以通过依赖注入的方式在其他组件中使用它们。
可以注入 `UserRepository` 并使用它

```java
@Autowired
private UserRepository userRepository
```

```
@Repository
public interface UserRepository extends CrudRepository<User,String> {
//UserRepository 作为一个接口，定义了对 User 实体进行 CRUD 操作的方法
}
```

如果此时调用save方法，它会按照CRUD里提供的方法进行操作



**@Query注解**
用于 自定义 数据库查询 方法
既然是自定义，那么我们需要声明SQL查询语句
方法名随意，但是最好符合规范

:parameter 在声明的SQL语句内作为占位符


```
    @Query("""
            select * from address a 
            where a.user_id =:userId
        """)
    List<Address> findByUserId(String userId);
```

在例子中，查询将返回一个 `Address` 对象的列表，每个对象都是根据查询结果集中的一行数据组装而成的
占位符那里，支持使用SpEL表达式 :#{#user.id} :声明占位符 #{声明这是EL表达式}



当你在继承了`CrudRepository`的接口中定义一个自定义查询方法时，你可以指定任何类型的返回值
`@Query`注解允许你编写自定义的JPQL（Java Persistence Query Language）或SQL查询语句。
查询结果映射是指将查询返回的结果集映射到指定的对象中。
这个指定的对象从哪知道？它怎么知道要映射到哪种对象里？我明明有那么多对象类

- **返回类型：** 你定义的方法的返回类型告诉Spring Data JPA你希望将查询结果映射到什么类型的对象
  例如，如果你的方法返回`List<AddressUserDTO>`，Spring Data JPA会尝试将查询结果的每一行映射到`AddressUserDTO`对象中

- **别名**：在JPQL查询中，你可以使用别名来指定查询结果的列名。这些别名应该与返回类型对象的属性名匹配。
  例如，在你的查询中，你使用了`a.id as id`，这意味着查询结果中的`id`列将被映射到`AddressUserDTO`对象的`id`属性
  已知返回类型为AddressUserDTO，那么查询结果会尝试映射到该对象中，我们为查询结果起名字为id，那么这个字段的结果就会尝试映射到AddressUserDTO中名为id的属性中
- **构造函数**：如果查询返回的是单个对象，Spring Data JPA会尝试使用返回类型对象的构造函数来创建对象。如果构造函数接受的参数与查询结果的列名匹配，那么这些列的值将被传递给构造函数。





**更新Update**

Spring -data-jdbc的更新操作同样基于save()方法，如果主键不存在则插入操作，如果存在则覆盖，也算是更新了
save方法按上面说的，会保存全部属性，对象的空值属性也会更新。因此更新局部属性时必须先查出全部属性，合并再更新
非常的麻烦，先查，再跟现在的对象合并，能不麻烦吗？现在有新的注解@Modifying
自动完成合并更新

```
@Modifying
@Query("SQL语句")
void update....
```

**删除delete**
删除数据 delete from 表名 where 条件
这个语句同样需要用到@Modifying注解

当你使用 `@Query` 注解执行自定义查询时，如果查询是修改数据的操作（如 `INSERT`、`UPDATE`、`DELETE`）
需要使用 `@Modifying` 注解来标记这个方法，不然报错，违反完整性，不给执行

普通的查询不需要这个注解，一旦涉及到数据更改，就要用这个注解



### 测试

在测试包test里创建对应的测试类，以User为例

```
@SpringBootTest
@Slf4j
class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void save(){
        var user = User.builder()
                .name("test2").build();
        userRepository.save(user);
    }
}
```

@SpringBootTest注解用于创建Spring容器，没容器怎么用Spring
@Slf4j 创建日志

测试类命名规范：将要测试的类名+Test

@Autowired 注解用于实现依赖注入，在其他需要用到该组件的地方也可以通过这个引入组件

UserRepository接口我们用@Repository把他放入了Spring容器里，现在通过这个注解把他注入
@Autowired会自动引入UserRepository类型的Bean，我们声明这个类型的变量，这个Bean就注入到这个变量里了
@Test用于标记一个方法为测试方法，然后写想测试的方法就行了
上面@Test表记 void save()方法为测试方法，要注意测试方法名是随意的，而且不需要有参数列表，我们只需要在测试方法里面通过注入进来的组件调用我们想要测试的方法就可以了





## SQL

SQL语句执行顺序

from
join
on
where
group by
having
select
distinct
order by
limit

当 order by 和 limit结合使用时，MySQL在确定了limit行后便不会排序了，不是全部排序完才limit的

### Explain

Explain是SQL查询计划分析工具，查询语句好不好 explain知道
SQL数据库会根据查询意图创建优化查询过程，并不是我们怎么写语句它就怎么查
咱们写的只是向SQL说明我们的意图，我们想干什么，具体怎么干由SQL决定

Explain输出包括执行成本/行数/时间/循环次数等相关信息

相关名词解释如下

驱动表：查询时先过滤的表，跟语句书写顺序无关，重申一下，我们写的只是意图

数据表访问方式 Type
Const 基于唯一索引检索
Eq_ref 连接时基于唯一索引检索
Ref 基于非唯一索引检索
Range 基于索引范围检索
Index 基于全索引检索
All  全表扫描

查询类型 Select_type
Simple 不含子查询的简单查询
Materrialized 物化子查询结果为临时表

![image-20241005144322704](https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241005144322704.png) 

在数据库的控制台里输入SQL语句后，在上面加一个explain，一起运行，注意一起运行
<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241005144417743.png" alt="image-20241005144417743" style="zoom:67%;" /> 

![](https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241005144528580.png) 

在result2里便可以看到本次查询的信息
查询了四行，全表扫描

```
explain
select * from user where id="1284873941642883072" ;
1,SIMPLE,user,,const,PRIMARY,PRIMARY,76,const,1,100,
可以看到这次扫描方式是 const 命中唯一索引

注意这里的id 如果不是 id="1284873941642883072" 而是 id=1284873941642883072
那么不会命中索引

MySQL里 id是String类型，现在传入int 未命中索引
MySQL里 id是 int 类型，现在传入 String可以命中索引，但是不推荐
最好是什么类型就传入什么类型的值
```



全表扫描的查询方式all是要极力避免的！
index 全索引扫描也是全表扫描，也要避免

### Status

查询数据库运行性能状态，掌握SQL语句具体执行情况
这个Status可以让我们看到SQL到底是怎么实现我们的意图的，用了哪些函数
Handler_read_key 命中索引次数
Handler_read_next 基于索引读取记录次数
Handler_read_rnd_next 没有命中索引读取数据的次数，也就是全表扫描的次数
Handler_writer 表（包含临时表）插入数据次数，涉及到写操作，占用资源就大了

怎么使用
先运行SQL语句，然后运行

```
show session status like "handler%";
```

想清空Status就使用

```
flush status;
```

![](https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241005145622556.png) 

但最好是 1.flush status 2.SQL语句 3.show ···

### 实例分析

现在有User表，Invi表，Detail表这个是中间表
Detail存两个表的主键，组合作主键，并对user_id,invi_id建立索引

需求：基于invi_id查询对应的user信息  invi_id=1对应2条detail记录，每个detail对应1条user记录，即一共2条user记录

```
explain
select * from user u
where exists
(select i.id from invi_detail i where u.id=i.user_id and i.invi_id="1")

explain
select * from user u
where u.id in
(select i.user_id from invi_detail i where i.invi_id="1")
```

这两种查询方法 exist和in，explain后发现结果是一样的
它俩的执行计划和效果相同，再次印证了我们写的只是意图 这个说法

![image-20241005211444293](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20241005211444293.png) 

select_type前面的数字代表查询顺序，越大越先查询，数字同样时上面的先执行查询
分析查询语句 Detail表
key: invi_id定位1次
Next:读取记录 2次
创建物化子查询临时表
write 写入子查询结果2次
Rnd_next 为与user表关联而全表无索引读取临时表3次User表
key 基于user_id定位2次

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20241005213252296.png" alt="image-20241005213252296" style="zoom: 67%;" />  

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20241005213413390.png" alt="image-20241005213413390" style="zoom: 67%;" /> 

这四种语句执行计划完全相同，说明执行与from,where的顺序无关，SQL根据过滤条件自己选择最优方案

### 设计

User一对多Address，Address一对一User
需求基于address id 查询地址以及对应用户的详细信息
实现1：由于address一对一user因此声明查询字段对应属性名称，创造AddressUserDTO类封装

```java
@Repository
public interface AddressRepository extends CrudRepository<Address, String> {

	@Query("""
        select a.id as id,a.detail as detail,u.id as userId,u.name as name,a.create_time as createTime,
           a.update_time as updateTime from address a join user u on a.user_id=u.id
        where a.id = :aid;
	""")
    AddressUserDTO findAddressUserDTOById(String aid);
}
```

上述查询结果为 id detail userId name createTime updateTime，想要映射的对象为 AddressUserDTO

在继承了CRUD的接口中，自定义查询的方法可以返回任何类型的值，只要你能正确映射

```
public class AddressUserDTO {
    private String id;
    private String userId;
    private String name;
    private String detail;
    private LocalDateTime createTime;
    private LocalDateTime updateTime;
}
```

名字符合映射规则的便会映射进去，组成一个AddressUserDTO类型的对象返回回去！

实现2：通过一次查询将结果分别封装在user/address对象中，再封装到一个DTO对象
这个没办法直接把查询结果映射了，映射只能映射到属性里，不能映射到对象里

```
public class AddressUserDTO2 {
    private User user;
    private Address address;
}
```

#### **RowMapper \<T> 接口** 

1. 现在有了新的接口 **RowMapper \<T> 接口** 
   可以用来自定义行映射规则 T指的是想要映射成的对象
   注意是Spring下的这个接口，别引入错了

2. 想使用这种方式，我们首先要定义一个新的类，然后让这个类实现这个接口，接口里的T是想要映射成的类型
   在这个实现类里重写映射方法： T mapRow（ResultSet rs，int rowNum）

```
public class AddressUserRowMapper implements RowMapper<AddressUserDTO2> {
    @Override
    public AddressUserDTO2 mapRow(ResultSet rs, int rowNum) throws SQLException{
            User user = User.builder()
                .id(rs.getString("u.id"))
                .name(rs.getString("name"))
                .createTime(rs.getObject("create_time", LocalDateTime.class))
                .updateTime(rs.getObject("update_time", LocalDateTime.class))
                .build();
            Address address = Address.builder()
                    .id(rs.getString("a.id"))
                    .detail(rs.getString("detail"))
                    .createTime(rs.getObject("create_time", LocalDateTime.class))
                    .updateTime(rs.getObject("update_time", LocalDateTime.class))
                    .userId(rs.getString("user_id"))
                    .build();
            return AddressUserDTO2.builder().user(user).address(address).build();
    }
}
```

要问查询结果集rs哪儿来的？你查询的时候会自动注入，不需要我们主动找。我们只需要告诉这个方法结果集的每一行应该怎么映射
这里看到结果集里的 u.id name ···放入User对象里， a.id detail···放入Address里，然后映射方法返回一个AddressUserDTO2的对象
到这里，新的映射规则就写好了，然后就是使用了



MySQL查询结果字段 在没有自定义映射名称时(没有用as时)的命名规则
非冲突字段 按实际字段名称，冲突字段以别名为前缀 “别名.字段"
比如两个表都有id，那么在结果集里分别为 表1.id 表2.id，如果只有一个表有id字段，那么结果集里就是id 



3. 在Query注解 显式声明 映射规则实现类

```
  @Query( value="select * from address a join user u on u.id=a.user_id where a.id=:aid",
    rowMapperClass = AddressUserRowMapper.class)
    AddressUserDTO2 findAddressUserByAid(String aid);
```

value属性用于指定查询语句，平时都是省略不写的
rowMapperClass 属性接收一个类对象，指定映射规则
 AddressUserRowMapper.class  .class用于获得一个类对象，传给这个映射规则属性
那么本次查询的每一行结果都会按照 AddressUserRowMapper这个类里的映射规则进行映射，用对应类型对象接收就行了



需求 基于用户ID获取用户基本信息以及所有信息地址

```
public class UserAddress {
    private User user;
    private List<Address> addresses;
}
```

想要通过用户ID查询到用户对应的所有address

方法一，单独定义一个返回值为List\<Address>的方法，拿到结果后跟User封装

```
    @Query("select * from address a where a.user_id=:userId")
    List<Address> findAddressByUserId(String userId);
    这个方法放在哪个组件里都行，放UserRepository可以，放AddressRepository也行
    
    @Test
    public void findAddressByUserId(){
    User user = userRepository.findById("userId");
    List<Address> addresses = addressRepository.findAddressByUserId("userId");
    UserAddress userAddress = UserAddress.builder().user(user).addresses(addresses).build();
    }
```

但是这样太慢了，我们需要方法二
明明一条SQL语句就可以查询出全部结果，但是默认结果集包含User冗余数据，并且无法自动映射封装
新接口来了

#### **ResultSetExtractor\<T>接口**

自定义 结果的映射实现规则  T仍然是想要映射成的对象类型
比如将多条记录映射为一个对象，组装一个集合

同样需要创建实现类，然后重写 T extractData(Result rs) 映射方法
这里传入的 ResultSet为整个结果集对象，不像RowMapper那里的rs只是结果集中的一行
这里虽然是整个结果集，但是游标在最上面，需要我们手动移动游标来获取每一行的信息

```java
public class UserAddressResultSetExtractor implements ResultSetExtractor<UserAddress> {//T是想要映射成的类型

    @Override
    public UserAddress extractData(ResultSet rs) throws SQLException, DataAccessException {
    //由于查询结果集中每一行的User都一样，所以我们只需要创建一次User对象就行了
    //先让User=null，当user=null时，我们封装一个user即可
        User user = null;
        List<Address> addresses = new ArrayList<>();
        while(rs.next()) {
            if(user == null) {
                user = User.builder()
                        .id(rs.getString("u.id"))
                        .name(rs.getString("name"))
                        .createTime(rs.getObject("create_time", LocalDateTime.class))
                        .updateTime(rs.getObject("update_time", LocalDateTime.class))
                        .build();
            }
            Address a = Address.builder()
                    .id(rs.getString("a.id"))
                    .userId(rs.getString("user_id"))
                    .detail(rs.getString("detail"))
                    .createTime(rs.getObject("create_time", LocalDateTime.class))
                    .updateTime(rs.getObject("update_time", LocalDateTime.class))
                    .build();
                    
            addresses.add(a);
        }
        return UserAddress.builder()
                .user(user)
                .addresses(addresses)
                .build();
    }//最后把两种封装起来返回去
}
```

在组件里仍然需要Query显式声明映射规则

```java
@Query(value=("select * from user u join address a on u.id=a.user_id where u.id=:userId"),
        resultSetExtractorClass = UserAddressResultSetExtractor.class
)
UserAddress findAddressByUserId(String userId);
```

然后测试

```java
@Test
void findAddressByUserId() {
    UserAddress userAddress = addressRepository.findAddressByUserId("1284873941642883072");
    log.debug(" debug: {}",userAddress.getUser());
    userAddress.getAddresses().forEach(a-> log.debug(" debug: {}",a));
}
```





### Pagination

分页
基于 MySQL limit 语句实现分页 `limit offset,size`
offset 偏移量。从offset位置后面计算
size offset后面的记录个数

```
@Query("""
   select * from user u 
    limit :offset,:pageSize
   """)
List<User> findAll(int offset, int pageSize);
```

 传入偏移量和页面size比如 
findAll(5,5)那么查出来5个，从5后数5个，也就是6-10
这个意思就是 每页5条记录，根据offset翻页

规范来写就像下面这样

```
int pageSize=5;
int page=4;
findAll((page-1)*pageSize,pageSize)
```

 (page-1)*pageSize 用于计算偏移量
第一页 page=1 算出来偏移量=0，那么第一页是 1-pageSize
第二页 page=2 算出来 偏移量就是pageSize，那么第二页就是pageSize+1 - 2\*pageSize

#### Pageable接口

Pageable接口 封装 offset/pageSize等分页数据
注意正确引入 ：springframework.data.domain.Pageable

PageRequest实现类，这个实现类可以直接用
PageRequest.of(int pageNumber,int pageSize) 根据指定的页数以及每页个数，封装计算limit的offset(我们不参与，它自己算)

```
@Query("""
   select * from user u 
    limit :#{#pageable.offset},:#{#pageable.pageSize}
   """)
List<User> findAll(Pageable pageable);
```

#{ } 声明SpringEL表达式
里面的#引用参数，通过对象.属性引用
SpringEL表达式没有自动提示



#### **Sorted**

MySQL order by 语句实现排序
order by 必须根据select中包含的字段排序
select中如果没有包含A，是不能通过A排序的 这个意思

```html
@Query("""
   select * from user u 
   order by u.id desc
    limit :#{#pageable.offset},:#{pageable.pageSize}
   """)
List<User> findByIdDesc(Pageable pageable);
```



## NoSQL

关系型数据库SQL是基于关系模式创建的二维表格模型，缺点：
结构化的数据模型不利于扩展与变更
不适合处理海量数据，不原生支持分布式集群···
范式强调减少冗余反而影响了查询效率

于是 非关系型数据库应运而生，用于储存非结构化数据的数据库系统
增强了数据的可扩展性，内存数据库增强了操作效率和速度

- 键值型数据库 Redis
- 文档型数据库 MongDB/Redis7
- 列祖型数据库 HBase

目前主流的关系型数据库都支持了json数据类型字段，因此SQL和NoSQL混合设计开发模式非常高效
通过冗余数据换取查询效率



### 实例

#### 教师数据库

教师信息数据库设计，需求
专业部门信息
教师，属于某一部门
需要加载指定部门的所有教师 功能
需要基于教师ID加载教师信息以及所属部门信息 功能

1. 如果按照范式设计
   部门表：部门信息
   教师表：教师信息+部门ID，在部门ID上面建立索引（因为不能用外键）
   				获取部门信息时必须并表查询
2. 反范式设计，愿意冗余
   部门信息不会经常变更，可以直接将部门信息以冗余信息的形式存储在教师表
   可以从教师表直接查询教师及部门信息而无需并表查询
   同时添加JSON类型中部门ID属性为索引，可通过部门ID获取全部教师而无需全表扫描

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241006144037941.png" alt="image-20241006144037941" style="zoom: 50%;" />   

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241006144112183.png" alt="image-20241006144112183" style="zoom:50%;" /> 

JSON Index
index(   (   cast(  department->>'$.depId' as char(19)   )    collate utf8mb4_bin   )   )
第一组括号：建立索引
第二组括号：声明索引表达式

department - >> '$.depId' 声明获取 JSON字段 department中的 depId属性值
并将值的双引号去掉，按照LONGTEXT类型返回utf8mb4_bin编码

 cast（··· as char(19)  ）函数 将值强制转换为char类型，而且还限制了长度为19捏
并且按照 utf8mb4_0900_ai_ci编码存储，此时与 ->>表达式结果编码不同

collate utf8mb4_bin  cast()函数按照指定编码存储，确保在查询时无需声明编码
`collate utf8mb4_bin`: 这部分指定了字符集和校对规则。`utf8mb4`是一种字符集

如果不强制声明cast（）函数存储编码就需要在查询语句里显式声明转换，否则无法命中索引



查询时也可以直接用JSON字段里的属性，同样需要双箭头

```
explain
select * from teacher t where t.department->>'$.depId'="1";

1,SIMPLE,t,,ref,functional_index,functional_index,79,const,1,100,
如果数据类型不匹配，查询也能查出来，但是不会命中索引！！！
结果正确但是效率低，这种情况很难发现，因此写时要注意类型
select * from teacher t where t.department->>'$.depId'=1;
1,SIMPLE,t,,ALL,,,,,1,100,Using where
```

JSON字段名 - >> '\$.键名' $代表根，取根下的键名对应的值



#### 打分表

毕业设计成绩由若干过程组成：开题/期中/毕业答辩等
每个过程包含若干比例的评分项：开题：报告50%前瞻创新型25%答辩说明25%
教师为学生的每个过程中的每个子项评分

按范式设计
过程表：包含过程名称/描述等 1:N过程项
过程项表：每个过程子项的详细信息：过程ID，项名称/描述等 1:1过程
评分表：教师ID/学生ID/子项ID/评分，唯一约束

3张表，5名教师为20名学生的开题评分（3子项）
那么有 5\*20\*3 = 300条记录 查询时还得并表查询

反范式冗余设计

过程表：将过程子项按JSON数组存储，比如过程“开题” 有三个子项：报告50%前瞻创新型25%答辩说明25%
评分表：过程ID/学生ID/教师ID，将教师每个过程子项评分和教师姓名以JSON冗余字段存储，唯一约束

2张表 5个教师为20学生开题评分，5*20 = 100条记录

过程表数据库设计
<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241008163654533.png" alt="image-20241008163654533" style="zoom: 50%;" /> 

items 子项，存过程子项名，占比，以及描述

打分表
<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241008164146554.png" alt="image-20241008164146554" style="zoom: 50%;" /> 

每名教师在每个过程下为每名学生的打分是唯一的，所以建立唯一索引，上面的index换成unique，便于查询



还有另一种方式
打分表中每个学生每个过程唯一，可以将教师id也扔进去
<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241008165952104.png" alt="image-20241008165952104" style="zoom:50%;" /> 



对于经常查但是不更新的数据，我们才考虑用JSON冗余存储，因为改JSON有点麻烦

# Spring

## Spring Framework

spring框架创建
仅需引入Lombok依赖，添加junit5运行时依赖和log配置即可创建
这是最基本的容器，所以什么也干不了



**IoC**控制反转
一种程序设计思想

控制：创建所需对象的控制权
反转：字面意思，主动/被动关系调转

本来我们需要什么对象，我们自己创建
现在控制反转，由程序创建对象，我们只需要拿过来用就行

**DI**
依赖注入，组件由容器管理，需要时由容器动态注入组件需要的其他组件

IoC == DI



由于组件就是用来注入使用的，所以组件中不能创建私有private方法



## **Component**

Spring容器中组件默认为单例模式

各种注解及作用？
@Component 声明为组件 
什么意思？意思是公共的服务，没办法归类为以下这些内容的方法放在这儿
比如 字符串大小写转换 ，它不属于下面几种组件任何一种，所以放这儿就好了

@Repository 声明为持久化组件

@Service 声明为业务逻辑组件

@Controller 声明为逻辑控制组件

@Bean  方法级 声明方法返回的对象由Spring容器管理

@Configuration 声明为配置类组件

组件注解有作用吗？有点，但不多
作用仅限于区分组件功能，让读者明白这个组件到底是干什么的
注解本身并没有特殊作用，因为它们的源码一模一样



### @Configuration

默认@Configuration注解修饰的类，会被创建代理对象并作为bean放在容器的配置组件里
这个注解是配置类注解，但他仍然算是一个组件,可以注入到其他地方使用
只是一般没人把这个注解类当组件用罢了

这个类里面的方法 boolean proxyBeanMethod() 默认返回值 true 用来创建代理对象的
这个代理对象没什么用，可以把这个返回值设置为 false 这样可以节省一些资源 (●'◡'●)
怎么设置？ @Configuration(proxyBeanMethod = false) 这样写注解就行了

这个类也算组件，所以不能有私有方法



### @Bean

类本身没有使用`@Configuration`注解
只要方法使用了`@Bean`注解，Spring容器在启动时会扫描带有`@Bean`注解的方法，并将这些方法的返回值注册为Bean

没有@Configuration注解，但是方法仍然会扫描并注册，那要这个注解有什么用？
没有使用这个注解，说明这个类不是组件，是非组件类，Spring不会自动向这个类里注入组件
那么如果@Bean修饰的方法使用到其他组件，但是这些组件没有注入，那么这个方法就不能正确执行，于是这个方法完蛋了

非组件类想用其他组件，必须手动申请注入



Bean是一种对象，生命周期由Spring容器管理
用注解修饰类后，Spring容器启动时会创建其实例并管理
其他Bean使用它时会自动注入给这些Bean，它使用其他Bean时容器也会自动注入给它

进一步说明，非组件类别想让Spring自动注入组件给你，Spring不会主动管你的

### 组件注入

#### @Autowired

基于类型注入
Spring容器会根据注入点类型（注解修饰的类型）查找容器中所有匹配该类型的Bean并注入
这种基于类型注入的方式不管Bean的名称，只关心其类型

#### 构造函数

Spring推荐使用基于组件的构造函数注入依赖的其他组件，因为它可以确保对象在使用之前已经完全初始化
我们之前是使用@Autowired 注解注入其他组件，但是这个仅推荐在测试里使用

假如我们有一个Example类，它依赖UserRepository和AddressRepository来实现功能

不注入

```
public class Example{
	
	private final UserRepository userRepository;
	private final AddressRepository addressRepository;

	不注入的情况下，我们需要手动实例化需要的类
	public Example(){
	this.userRepository=new UserRepository();
	this.addressRepository = new AddressRepository();
	}
	
	public void method(){
	userRepository.find();
	return;
	}
}
```

使用构造函数注入组件↓ 

```
@Component
public class Example{
	
	private final UserRepository userRepository;
	private final AddressRepository addressRepository;
	
	当我们实例化Example时，Example的构造函数里两个参数对象不是我们自己创建的，我们并没有new一个实例。
	那这个实例是从哪儿来的？是容器注入的，这就是注入，不需要我们自己创造对象
	
	public Example(UserRepository userRepository,AddressRepository addressRepository){
	this.userRepository=userRepository;
	this.addressRepository = addressRepository;
	}
	
	public void method(){
	userRepository.find();
	return;
	}
}
```

**final**

final 修饰的字段在表示一旦这个变量被初始化赋值后，它的值就不能再被改变
也正因为 final字段的不变性，导致final修饰的字段在构建对象前**必须被初始化**

final字段初始化有两种方式：
1.构造函数里初始化 
2.声明时直接初始化   private final int value = 42; 

如果你既没有在声明时直接初始化`final`字段，也没有在构造函数中为它赋值，那么编译器将会报错
因为`final`字段必须在对象构造完成之前被初始化！！！



那么我们通过把组件声明为final，那么保证了该类实例化成对象的话，一定已经加载好了它依赖的其他组件。
换个说法就是 依赖组件成功注入类中。

但是手动写构造函数很麻烦，如果后来需要增加组件，那么也要在构造函数里手动写。
我们能不能通过注解比如@AllArgsConstructor使编译时自动创建构造函数？
可以的，但是我们并不需要用到全参构造函数，我们可以使用@RequiredArgsConstructor注解
这个注解会创建由必需属性组成的构造函数以及无参构造函数
必须属性也就是由 final 修饰的属性
达到了自动创建组件构造函数的目的

```
@Component
@RequiredArgsConstructor
punlic class Example{
	private final UserRepository userRepository;
	private final AddressRepository addressRepository;
	
	public void method(){
	userRepository.find();
	return;
	}
	
}
```

在 `Example` 类的 `method` 方法中，可以直接调用 `userRepository` 的 `find` 方法
因为 `userRepository` 已经被注入到 `Example` 类的实例中
Example 类创建实例时，依赖已经通过构造函数注入该实例了，所以该实例可以使用  userRepository的方法，没疑惑了吧



Spring容器启动时，扫描并创建指定路径下全部组件的实例
并且以键值对的形式保存实例，键为 类名且首字母小写形式保存，值就是容器创建的对象
所以当你的组件里存在同名组件时，会报错，容器启动异常
就算同名组件不在同一个路径下，它生成的实例也会放到Spring容器里导致重名
所以默认情况下，不要声明同名组件

真想整同名组件，你就要显式指定这个组件名称
在组件注解括号里写上你想命名的名字 比如

```
A包下
@Repository("dao.userdao")
public class UserDao{}
B包下
@Repository
public class UserDao{}
```



Spring框架中，组件通常不是以接口形式存在的，而是以类的形式存在
我们把类声明为组件，使用时可以直接创建类的对象

当你声明一个接口为Spring组件，并且没有显式地提供一个实现类时
实际上你通常是在使用Spring Data JPA或者其他类似的Spring框架特性，这些框架会在运行时自动为你生成实现类

以Spring Data JPA为例，当你声明一个接口并让它扩展了`Repository`或其子接口（如`CrudRepository`、`JpaRepository`等）
Spring Data JPA会在运行时动态地为你的接口创建一个代理实现类。
这个代理类实现了接口中定义的所有方法，包括你使用`@Query`注解自定义的查询方法。

如果基于接口类型注入对象，但是同时存在多个实现类，那么容器会抛出异常，因为不知道要注入哪个实现类对象
我们可以对其中一个实现类使用@Primary注解，这样的话，注入时会选择这个实现类

当我们使用@Autowired基于类型注入，但是需要选择一个实现类时，需要使用@Qualifier注解声明对象名称
这个优先级比 @Primary高，即使当时有 其他实现类注解了@Primary，它也会选择@Qualifier指定的实现类注入

```
@Autowired
@Qualifier（实现类名）
private UserRepository userRepository;
```





如果想让Spring容器自动注入组件，需要把这个类声明为组件，如果它不是组件类，那么Spring不会把组件注入进去

当然，非组件类也可以手动获取容器中的Bean，或者用@Autowired注解使用容器中的组件
如果你不想使用`@Autowired`或手动获取Bean，那么非组件类将无法直接使用Spring容器中的组件。
上面的通过构造函数获得组件也当然不行。



### @value

@Value  修饰组件属性，可以基于SpEL表达式注入值（如配置文件中的自定义值等）
${ } 引用 application.yml配置中声明的变量

```
@Component
public class Example{
	@Value("${my.secretkey}")
	private String secretkey;
}
这个注解会把application.yml里这个值拿过来注入到这个属性里
application.yml里
my:
  secretkey: ABCD
```

避免以硬编码形式放入代码中
我们可以把一些token/第三方密钥等声明在配置文件里，然后github ignore这个配置文件，达到保密效果



### Events

Spring容器运行生命周期会触发一系列事件，可以通过指定事件监听器监听所需事件
@EventListener 指定监听事件类型，回调执行修饰的方法
支持自定义监听事件

有些初始化数据必须通过业务（java）添加，比如密码，总不能让SQL语句作运算
因此可以通过容器启动监听器完成数据记录初始化，从而降低数据库部署难度，增加项目可维护性





### 实例

```
package org.example.jdbcexamples.repository;

import org.springframework.stereotype.Component;

@Component
public class Demo {
    public void demo() {
        System.out.println("注入成功");
    }
}
```

DemoTest 依赖于 demo ，需要注解DemoTest为组件才能让 容器通过构造函数注入
同时使用Required注解记得把 demo 用final修饰

```
package org.example.jdbcexamples.repository;

import lombok.RequiredArgsConstructor;
import org.springframework.stereotype.Component;

@RequiredArgsConstructor
@Component
public class DemoTest {
    private final Demo demo;

    public void demoTest(){
        demo.demo();
    }
}
```

然后使用DemoTest时，不要
DemoTest demoTest = new DemoTest();这样就白费了
你手动创建的实例是无参的，需要用的是容器注入进来的demoTest

你应该是让容器给你注入一个

@Autowired
DemoTest demoTest；

然后直接使用demoTest，而不是自己创建一个没用的对象

```
package org.example.jdbcexamples.repository;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

import static org.junit.jupiter.api.Assertions.*;

@SpringBootTest
class DemoTestTest {

    @Autowired
    private DemoTest demoTest;

    @Test
    void demoTest() {
        demoTest.demoTest();
    }
}
```





## Mockito

### 问题

在单元测试时，如果依赖的服务未开发完成，或者依赖的对象不方便构造，可以通过Mock模拟组件对象

解决问题：
A依赖B，但是B没开发完，那么如何对A进行单元测试？
如果A需要等B开发完才能测试，那这还能叫并行开发吗？

```
@Repository
public interface UserRepository{
	User save(User user);
	
	User findById(String id);
}
```

以上这个接口声明为组件，但是没有继承CRUD接口，那么Spring不会对它自动创建一个代理的实现类
也就是说，这个接口根本没开发完

```
@Service
@Slf4j
@RequiredArgsConstructor
public class UserService{
	private final UserRepository userRepository;
	
	public User addUser(User user){
		return userRepository.save(user);
	}
	
    public User findById(String uid){
    	return userRepository.findById(uid);
	}
}
```

这个业务依赖的User组件未开发完成，那么如何测试这个组件？



### @MockBean

@MockBean 由它声明修饰的组件将由 Mock框架创建模拟对象，而非注入真实的组件对象

```
@MockBean
private UserRepository userRepository;
```

这个注解修饰这个组件，Mock框架会模拟一个对象注入进来，但是注入进来的是假的！！！
就算这个组件已经完成了，它仍然会注入一个假的，跟真实存在的这个组件一点关系都没有

测试

```
@SpringBootTest
@Slf4j
class UserServiceTest{
	@MockBean
	private UserRepository userRepository;
	模拟下面要测试的组件需要的组件
	@Autowired
	private UserService userService;
	注入要测试的组件
}
```



Mockito的方法

when( ) 模拟Mock组件方法调用
anyX( ) 模拟调用Mock对象方法时传入的参数
thenReturn( ) Mock组件方法调用时的返回值
thenThrow( ) Mock组件抛出指定异常对象
thenAnswer( ) Mock组件方法调用时执行操作，里面放入一个函数可以是箭头函数，组件方法调用就会执行函数

```
@Test
void getUser(){
	Mockito.when(userRepository.findById("1"))
	//when方法，模拟调用了组件的方法
	//假装我们调用了，然后我们既然调用了这个方法，那么我们需要假装返回了一个值
		   .thenReturn(User.builder().id("1").name("P").build());
		   //假装返回值，实际上并没有返回值让我们用，所以连返回值也需要我们模拟
		   //按照这个方法预定的返回值类型模拟，不是让你乱模拟
		   
	上述两句的意思是，当我们调用这个方法且传入参数为字符串1时，便会返回一个 id=1 name=p的User对象
	
	User u = userService.getUser("1"); 这里调用了 userRepository.findById("1"),那么会返回上述对象
	log.debug("{}",u);
	// id=1.name=p
	
	
	User u2 = userService.getUser("2");
	//这里想调用 userRepository.findById("2"),但是我们没有模拟这个方法，没有返回值
	log.debug("{}",u2)
	// null
}
```



anyX( )使用

```
@Test
void getUser() {
    Mockito.when(userRepositoryMock.findById(Mockito.anyString()))//这里用到了anyX，X是String
            .thenReturn(User.builder().id("1").name("Pang").build());
    意思是，调用userRepositoryMock.findById(任意字符串参数)，都会返回上述对象
    User u = userService.getUser("1");
    User u2 = userService.getUser("2");
    上述两种调用全符合我们设置的when 所以都会返回设置的模拟值
    System.out.println(u.toString()); //User(id=1, name=Pang, createTime=null, updateTime=null)
    System.out.println(u2.toString()); //User(id=1, name=Pang, createTime=null, updateTime=null)

}
```





# SpringMVC

SpringMVC项目创建
<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241010224930989.png" alt="image-20241010224930989" style="zoom:50%;" /> 
右键工作区，选择新建模块
SpringMVC只需要

- Lombok
- Spring Web

两个依赖就可以了，后期需要其他的再加
其实还有一个依赖可以选：SpringBoot devtools 这样页面失去焦点就会重新渲染，热部署，不用我们重启项目
这个依赖更适合开发环境，学习环境下用不上这个，每次改东西后手动重启就行

之前交互是一个Servlet类指定处理对一个路径的请求
现在SpringMVC，容器启动时，扫描到Controller组件，注册controller里的 请求处理方法
匹配到HandlerMapping

Dispatcher(分发器)  拦截所有请求，然后再内部判断转发到哪个组件处理，这个是**所有请求的入口**
Dispathcer调用 HandlerMapping 查找与请求相匹配的Controller组件，并将对应请求发送到这个组建的方法处理处  **这个是转发**

Controller方法调用业务逻辑组件处理业务逻辑，然后序列化返回的数据，返还给请求方   **这个是处理**



## RESTful

REpresentational State Transfer (REST) or RESTful，一种思想

Resources 资源，网络上的任何信息实体，文章/图片/音乐/服务都可以算是资源
而每个资源都有唯一的URL

Representation 表现 每个资源都有多种外在表现形式
例如服务器可以以HTML王爷的形式把多种形式的资源发送给客户端

State Transfer 状态转化，客户端基于无状态的HTTP协议，通过HTTP GET/POST/PUT/PATCH/DELETE
请求动作描述对资源的操作，从而完成互交

REST API ，用这个统一的协议，数据库可以为所有终端梯控数据服务，各终端根据自己的形式渲染数据

REST规范要求 请求中包含状态，而不是让服务器保存状态
服务器不再使用HTTP session维护(保存)客户端的状态
RESTful是一种鞥个而不是标准
默认浏览器仅能发送 GET/POST请求。因此基于浏览器的请求需要通过JS完成

## Github RESTful API

- GET

  获取全部仓库下/指定用户/指定仓库/全部议题下/指定议题内容
  /repos/{:owner}/{:repo}/issues/{:number}

  获取全部仓库下/指定用户/指定仓库/全部议题下/指定议题/全部评论
  /repos/{:owner}/{:repo}/issues/{:number}/comments

- POST

- PATCH

- DELETE



## Jackson

Java Json解析框架，提供将Java对象序列化/反序列化为json对象等
序列化：把java对象转换成Json对象，也就是用纯字符串描述java对象
反序列化：把json对象转换为java对象，把纯字符串转化为java对象

Json这种纯字符串的对象使得不同语言的对象能够相互传递

## Mapping

@Controller 声明为控制层组件，默认返回视图

@RestController 默认组件中全部方法返回  序列化的json数据
组件中的方法返回值最终会 变成json数据返回去

@RequestMapping 请求映射，类型级方法级，可用于给组件提供一个根路径

@GetMapping/@PostMapping/@PatchMapping/@PutMapping/@DeleteMapping
修饰组件中的方法，分别处理对应的HTTP请求类型

Controller组建的一个方法就可以处理一个请求，而Servlet类最多处理一个GET+一个POST
因此两个 controller方法就能实现一个Servlet的功能

```
@RequestMapping("/api/")//  /api/是这个组件的根路径，组件内所有注解内的路径都会与其拼接后使用
@RestController
public class example {

    @GetMapping("address")  //   处理 项目部署根/api/address路径的Get请求
    public Address getAddress(){
        return Address.builder().detail("string").build();
    }
由于组件用RestController注解，返回值会变成json对象
}
```

项目启动后访问这个地址可以看到结果，注意是启动下面这个的 main函数
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20241011110204940.png" alt="image-20241011110204940" style="zoom:50%;" /> 

然后浏览器输入 localhost:8080/ 这是服务器根
localhost:8080/api/address
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20241011110312598.png" alt="image-20241011110312598" style="zoom:67%;" /> 页面显示这个json对象
