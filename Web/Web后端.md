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

![image-20240918172217331](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240918172217331.png)

logging:level，声明不同包的路径日志级别，root为最顶层节点，声明root全局warn以上级别输出
下面的那个则声明 com.example下的日志输出等级为debug，输出日志时只能输出debug及更高级的日志



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

