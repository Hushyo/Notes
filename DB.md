## 1.1数据库概述

### 1.1.1四个概念

#### 数据

- 定义：数据（Data）是数据库中存储的基本对象

- 特点：数据的含义称为数据的语义，数据与其含义是不可分的。
- 种类： 文本、图形、图像、音频···

#### 数据库

Data Base --- DB

- 定义：数据库是**长期存储**在计算机内,**有组织的,可共享的**大量数据的集合
- 基本特征：具有较小的冗余度，较高的数据独立性和易扩展性,可为各种用户共享
- 三个基本特点：**永久存储，有组织，可共享**

#### 数据库管理系统

Data Base Management System --- DBMS

- 定义： 位于 用户 与 操作系统 之间的一层数据管理软件
  是基础软件，是一个大型复杂的软件系统
- 用途：科学地 组织和存储 数据，高效地 获取和维护 数据

#### 数据库系统

Data Base System --- DBS

- 定义： 在计算机系统中引入数据库后的系统构成数据库系统

### 1.1.2数据管理技术的发展

数据管理是指对数据进行分类,组织,编码,存储,检索,和维护.它是数据处理的中心问题.
数据管理技术经历了 **人工管理,文件系统,数据库系统** 三个阶段

### 1.1.3数据库系统的特点

#### 数据结构化

数据库系统实现整体数据的结构化.
这是数据库的主要特征之一.也是数据库系统与文件系统的本质区别

#### 数据的共享性高,冗余度低且易扩充

数据共享可以大大减少数据冗余,节约存储空间,数据共享还能避免数据之间的不相容性与不一致性

> 数据不一致性指的是 同一数据不同副本的值不一样

#### 数据独立性高

数据独立性是数据库管理的一个显著优点.
数据独立性包含数据的 物理独立性 和逻辑独立性

物理独立性 指用户的应用程序与数据库中的数据的物理存储是相互独立的.
数据在数据库中怎样存储由数据库管理系统管理,用户不需要了解

逻辑独立性 指用户的应用程序与数据库的逻辑结构是相互独立的
数据的逻辑结构改变,用户程序可以不变

#### 数据由数据管理系统统一管理和控制

数据库的共享会带来数据库的安全隐患,而数据库的共享是 并发的共享
数据库中数据的正确与一致必须保障

> 并发的共享:多个用户可以同时存取数据库中的数据

为此 数据库管理系统必须提供下面的数据控制功能:

1. 数据的 安全性保护
2. 数据的 完整性检查
3. 并发控制
4. 数据库恢复









## 1.2数据模型

- 数据库中用数据模型来 抽象、表示和处理现实世界中的数据和信息。
  通俗来讲，数据模型就是对现实世界的模拟
- 数据模型应满足三方面要求：比较真实模拟现实世界，容易被人理解，容易在计算机上实现

- **数据模型是数据库系统的核心和基础**
- 数据模型划分为两大类
  第一类是 **概念模型**,第二类是**逻辑模型和物理模型**
  概念模型又称为信息模型，用于数据库设计
  逻辑模型包括 网状模型，层次模型，关系模型，面向对象模型，用于DBMS实现。

### 1.2.1概念模型

#### 基本概念

##### 实体 entity

> 核心

客观存在并且可互相区分的实物称为实体.

> 可以是 人 事 物 也可以是抽象的概念或联系 如 一个学生,学生的一次选课,教师与院系的关系··

##### 属性 attribute

实体所具有的某一特征称为属性一个实体可以由若干个属性来刻画.

> 学生实体可以由 学号 性别 姓名 出生年月 院系 入学时间等组成 

##### 域 Domain

属性的取值范围称为该属性的域

##### 码 key

唯一标识实体的属性集 称为 码

> 学号是学生实体的码 

##### 实体型 entity type

具有相同属性的实体必然具有共同的特征和性质.
用 实体名及其属性名集合来抽象和刻画同类实体,称为实体型

> ?学生(学号,姓名,性别,出生年月,院系.入学时间)  就是一个实体型

##### 实体集 entity set

同一类型的实体的集合称为实体集

> 全体学生

##### 联系 relationship

联系在信息世界中反应为 实体(型)内部的联系 和 实体(型)之间的联系
内部联系通常指组成实体的各个属性之间的联系
实体之间的联系通常是指不同实体集的联系

联系有三种

![QQ图片20240411184441](https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/QQ%E5%9B%BE%E7%89%8720240411184441.png)

#### E-R图

- 概念模型的一种表示方法。
  该方法用 **E-R图**来描述现实世界的概念模型
  **E-R方法也称为E-R模型**

- 实体型 用矩形表示，框内写明实体名。
  属性 用椭圆表示，框内写明属性名。
  联系 用菱形表示，框内写明联系名。（联系也可以有自己的属性）
  三者用无向边进行连接，注意表上几对几

  ![QQ图片20240411185100](https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/QQ%E5%9B%BE%E7%89%8720240411185100.png)

> 联系供应有自己的属性供应量

### 1.2.2组成要素

#### 数据结构

数据结构描述数据库组成对象，及对象之间的联系。
数据结构是对**系统静态特性**的描述

#### 数据操作

数据操作是指对数据库中各种对象的实例允许执行的操作的集合，包括操作及有关的操作规则
数据库主要有 **查询和更新(插入,删除,修改)** 两大类操作
数据操作是对**系统动态特性**的描述

#### 数据的完整性约束条件

一组完整性规则的集合
完整性规则是给定的数据模型中数据及其联系所具有的制约和依存规则。
用来限定符合数据模型的数据库状态以及状态的变化

### 1.2.3逻辑模型

#### 层次模型

数据库系统中最早出现的数据模型，用树形结构表示实体，和实体之间的联系。
条件：有且只有一个节点没有双亲，称为根节点，根以外的其他节点有且只有一个双亲节点
			上层类型和下层类型是1:n的联系

特点：结点的双亲是唯一的。只能直接处理一对多的实体联系
			任何记录只有按路径查看时才能显示出意义
			没有子记录值能脱离双亲记录值而独立存在
			每个记录类型可以定义一个排序字段，也称为码字段
完整性约束条件：
			无相应的双亲结点值，不能插入子结点值
			如果删除双亲结点值，相应的子结点值也被同时删除
优点：查询效率高，数据结构简单清晰，提供良好的完整性支持

缺点：多对多联系表示不自然
			插入和删除操作的限制多
			查询子女必须通过双亲结点

![QQ图片20240411211022](https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/QQ%E5%9B%BE%E7%89%8720240411211022.png)

#### 网状模型

采用网状模型作为数据的组织方式
是满足下面两个条件的 基本层次联系 的集合：
1.允许一个以上的结点无双亲结点 
2.一个结点可以有多个双亲结点和多个子女结点 
3.有向图中的结点时记录类型，有向边表示从箭尾一端的记录类型到箭头一段的记录类型间的1:n类型，
   箭尾表示双亲，箭头表示子女结点

>  网状模型和层次模型的区别
> 网状模型允许多个结点没有双亲，允许结点有多个双亲，允许结点间有多种联系
> 层次模型实际上是网状模型的一个特例

![QQ图片20240411213209](https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/QQ%E5%9B%BE%E7%89%8720240411213209.png)

特点：可以插入无双亲的结点
			删除双亲后，子结点可以存在
			更新操作简单
			查询操作有多种实现方法
优点：更直接描述现实世界，如一个结点可以有多个双亲。
			具有良好的性能，存取效率高
缺点：结构比较复杂，不利于最终用户掌握


#### 关系模型

用户观点下是二维表，由行和列组成

- 关系





## 3.1SQL

### 3.1.1 Development

···

### 3.1.2 SQL特点

- 功能综合且风同一
- 数据操纵高度非过程化
- 面向集合的操作方式
- 以统一的语法接口提供多种使用方式
- 语言简洁，易学易用

### 3.1.3 SQL概念

- **基本表**
  本身独立存在的表。
  关系数据库管理系统中一个关系对应一个基本表
  一个或多个基本表对应一个存储文件
  一个表可以带若干索引
- **存储文件**
  逻辑结构和物理结构组成了关系数据库的内模式
  物理文件结构由于DBMS设计确定
- **视图**
  从基本表或其他视图中导出的表
  数据库中只存放视图的定义而不存放视图对应的数据
  视图是一个虚表
  视图上可以再定义视图

## 3.2数据定义

SQL数据定义功能：表定义、视图定义、索引定义。

![QQ图片20240411213209](E:/PS/08stu/QQ%E5%9B%BE%E7%89%8720240411213209.png)

<font color=red>不分大小写，不论是方法还是表名，（列名分）。</font>
创建表 student 和 Student STUDENT 其实都是同一个表

### 3.2.1  模式

#### **定义**

<font color=blue>CREATE SCHEMA \<模式名> AUTHORIZATION \<用户名></font>
如果不指定模式名，模式名隐含为用户名

```sql
CREATE SCHEMA "S-C-SC" AUTHORIZATION WANG;
为用户 WANG 定义了一个模式 S-C-SC
CREATE SCHEMA  AUTHORIZATION WANG;
为用户 WANG 定义一个模式 没写模式名，那模式名就是 WANG
```

- 定义模式实际上定义了一个命名空间
- 空间中可以定义该模式包含的数据库对象：如基本表，视图，索引···

#### **删除**

<font color=blue>DROP SCHEMA <模式名> <CASCADE|RESTRICT></font>
CASCADE（级联）：强制删除
删除模式同时把该模式中的数据库对象全部删除
RESTRICT（限制）：如果该模式中有数据库对象，则拒绝执行删除语句
仅当模式中没有任何下属的对象时才能执行

```sql
DROP SCHEMA Test CASCADE;
删除模式Test，Test中定义的东西也都没了
```

### 3.2.2 基本表

#### **定义**

<font color=blue>CREATE TABLE <表名> （</font>
<font color=blue><列名> <数据类型> [列级完整性约束条件],</font>
<font color=blue><列名> <数据类型> [列级完整性约束条件],</font>
<font color=blue><列名> <数据类型> [列级完整性约束条件],</font>
<font color=blue>[<表级完整性约束条件>]);</font>

> < 必选项 >，[ 可选项 ]。
> 完整性约束条件：表中数据要满足的条件

- **模式与表**
  每一个基本表都属于一个模式，一个模式可以包含多个基本表

#### **数据类型**

定义数据时，要指明数据的 **类型** 和 **长度**

|               类型               |                             含义                             |
| :------------------------------: | :----------------------------------------------------------: |
|    CHAR（n）, CHARACTER（n）     |                     长度为n的定长字符串                      |
|   VARCHAR（n），VARCHAR2（n）    |                   最大长度为n的变长字符串                    |
|               CLOB               |                         字符串大对象                         |
|               BLOB               |                         二进制大对象                         |
|           INT，NTEGER            |                  整数，范围[-2^31^,-2^31^]                   |
|             SMALLINT             |                 短整数，范围[-2^15^,-2^15^]                  |
|              BIGINT              |                 大整数，范围[-2^63^,-2^63^]                  |
|          NUMBER（p，d）          | 定点数，由p位（不含符号，小数点）数字组成<br />小数点后有 d 位数字 |
| DECIMAL（p，d）<br />DEC（p，d） |            同NUMERIC相似，但数值精度不受p，d限制             |
|               DATE               |           日期，包含年月日<br />格式 ：YYYY-MM-DD            |
|               TIME               |            时间，包含时分秒<br />格式 ：HH:MM:SS             |
|             BOOLEAN              |                          逻辑布尔量                          |
|            FLOAT（n）            |              可选精度浮点数，精度至少为n位数字               |
|               REAL               |                 取决于机器精度的单精度浮点数                 |
|         DOUBLE PRECISION         |                 取决于机器精度的双精度浮点数                 |
|            TIMESTAMP             |                          时间戳类型                          |
|             INTERVAL             |                         时间间隔类型                         |

#### **完整性约束条件**

完整性约束条件是指数据要满足的条件
完整性约束条件被存入系统的数据字典中，当用户操作表中数据时，由DBMS检查是否违背完整性约束条件
完整性约束条件设计表的多个属性列时，必须定义在表级上
完整性约束条件只涉及一个属性列时，可以定义在表级上，也可以定义在列级上

- **主码约束**

  ```sql
  #建立一个课程表Course，由课程号Cno、课程名Cname、先行课程和Cpno、学分Ccredit四个属性构成
  CREATE TABLE Course(
  Cno number(4) constraint pk_Course primary key,
  Cname char(20),
  Cpno number(4),
  Ccredit number(4));
  #将列级条件改为表级条件
  #表级约束：写完约束后括号（属性，属性），表明约束哪些属性，用逗号隔开多个属性
  CREATE TABLE Course(
  Cno number(4) ，
  Cname char(20),
  Cpno number(4),
  Ccredit number(4)，
  Constraint pk_Course primary key(Cno));
  ```

  

- **外码约束**

  ```sql
  #表级外码约束
  CREATE TABLE SC(
  Sno number(12),
  Cno number(4),
  Grade number(3),
  Constraint pk_SC primary key(Sno,Cno)，
  Constraint fk_c foreign key(Cno) references Course(Cno)); 
  #改为列级外码约束
  CREATE TABLE SC(
  Sno number(12),
  Cno number(4) Constraint fk_c references Course(Cno),
  Grade number(3),
  Constraint pk_SC primary key(Sno,Cno));
  #外码可以参照自身
  CREATE TABLE Course(
  Cno number(4) constraint pk_Course primary key,
  Cname char(20),
  Cpno number(4) Constraint fk_cpno references Course(Cno),
  Ccredit number(4));
  #Cpno字段，参照于 Course 表中的 Cno 字段
  ```

- **CHECK约束**

  ```sql
  #检查成绩
  CREATE TABLE SC(
  Sno number(12),
  Cno number(4),
  Grade number(3) Constraint ck_g check(Grade>=0 AND Grade<=100),
  Constraint pk_SC primary key(Sno,Cno),
  Constraint fk_s foreign key (Sno) references Student(Sno),
  Constraint fk_c foreign key (Cno) references Course(Cno));
  #检查性别只能是男或女
  CREATE TABLE TEST(
  id number(2) primary key,
  name varchar2(20),
  sex char(2) check(sex in ('男','女')));
  ```

- **NOT NULL 约束**

  ```sql
  CREATE TABLE Course(
  Cno number(4) constraint pk_Course primary key，
  Cname char(20) not null,
  Cpno number(4),
  Ccredit number(4));
  ```

- **UNIQUE 约束**

  ```sql
  CREATE TABLE Course(
  Cno number(4) constraint pk_course primary key ，
  Cname char(20) constraint u_cname unique,
  Cpno number(4),
  Ccredit number(4));
  ```

  多列设置唯一，表级约束 unique(列1，列2)

- **DEFAULT约束**

  ```sql
  CREATE TABLE Student(
  Sno number(12),
  Sname char(20),
  Ssex char(2) default('男'),
  Sage number(3).
  Sdept char(10));
  ```

#### 修改

<font color=blue>ALTER TABLE <表名> </font>
<font color=blue>[ADD <列名> <数据类型> [完整性约束条件]]</font> 添加多个用括号
<font color=blue>[DROP column <列名>]</font> 删除单列 要column
<font color=blue>[DROP (列名1，列名2)]</font> 删除多列 不要column
<font color=blue>[ADD constraint <完整性约束条件名><完整性约束条件>]</font>
<font color=blue>[DROP constraint <完整性约束条件名>]</font>
<font color=blue>[MODIFY <列名> <数据类型> [完整性约束条件] ]</font> **;** 修改列名数据类型为这个新的数据类型，改多列用括号

```sql
#向学生表中加入入学时间和生源地属性
ALTER TABLE STUDENT ADD
(S_entrance date,
S_source char(20));
#删除入学时间
ALTER TABLE STUDENT DROP COLUMN S_entrance;
#删除入学时间和生源地
ALTER TABLE STUDENT DROP (S_entrance,S_source char);
#修改 Ssex 数据类型 改为 char（8）且加入默认约束 女
ALTER TABLE STUDENT MODIFY Ssex char(8) default('女')
#删除约束
ALTER TABLE SC DROP CONSTRAINT ck_g; ck_g 是约束名
ALTER TABLE STUDENT DROP UNIQUE(Sname); 删除唯一值约束
```

> 删除约束要小心，比如删除 unique或者 primary key 时可能删除相关索引

#### 删除

<font color=blue>DROP TABLE <表名></font>

```sql
DROP TABLE STUDENT;
```

#### 插入数据

<font color=blue>INSERT INTO <表名>(列名1，列名2，列名3)</font>
<font color=blue>VALUES (具体属性);</font>

```

```



### 3.2.3 索引

- 建立索引目的 ：加快查询速度

- 常见索引：
  顺序文件上的索引
  B+树索引
  hash索引
  位图索引
- 特点：
  B+树索引具有动态平衡的特点
  哈希索引具有查找速度快的特点
- 谁建立谁删除：数据库管理员或者建表人
  谁维护索引：数据库管理系统自动完成
  使用索引：关系数据库管理系统自动选择合适的索引作为存取路径

#### 建立索引

想建立一个索引，首先需要一个表。在语句中，告诉数据库创建的新索引的名称，在哪个表上建立，包含哪些列。
<font color=blue>CREATE [UNIQUE] INDEX <索引名> ON <表名> (<列名> [次序]，<列名> [次序]，)；</font>
次序用来指定索引值的排列次序，包括ASC(升序)和DESC(降序)，不写默认ASC
UNIQUE表明此索引的每一个索引值值对应唯一的数据记录

```sql
#为COURSE SC表建立索引 COURSE按课程名升序建立唯一索引 SNO CNO按学号升序和课程号降序建立唯一索引
CREATE UNIQUE INDEX Coucname ON Course(Cname);
CREATE UNIQUE INDEX Scno ON SC(Sno ASC,Cno DESC);
```

#### 删除索引

<font color=blue>DROP INDEX <索引名> </font>

```sql
#删除COURSE 表的 CNAME索引
DROP INDEX Coucname
```

### 3.2.4数据字典

数据字典记录了数据库中所有定义信息
关系模式定义	视图定义	索引定义
完整性约束定义	各类用户对数据库的操作权限	统计信息···

## 3.3 数据查询

<font color=blue>SELECT [ ALL | DISTINCT ]<目标列表达式> [,目标列表达式,目标列表达式···]</font> 想要查询的列，可以是多列
<font color=blue>FROM <表名或视图名> [,<表名或视图名>,<表名或视图名>···]</font>
<font color=blue>[WHERE <条件表达式>]</font>
<font color=blue>[GROUP BY <列名> [HAVING <条件表达式> ] ]</font>
<font color=blue>[ORDER BY <列名> [ ASC | DESC ] ]</font>
<font color=blue>LIMIT <行数1> [OFFSET <行数2> ];</font>

SELECT ：指定要显示的属性列
FROM ：指定查询对象（基本表或视图）
WHERE：指定查询条件
GROUP BY：结果按照 列名 的值进行分组，该属性列值相等的元组为一个组
HAVING：满足指定条件的组才能输出
ORDER BY ：对查询结果按 列名 的值进行升序|降序排序
LIMIT 限制SELECT查询结果的数量为<行数1>行
OFFSET 表示在LIMIT计算<行数1>前忽略<行数2>行

### 3.3.1 单表查询

**查询仅涉及一个表**
选择表中若干列
选择表中若干元组（行）
ORDER BY子句
GROUP BY 子句
LIMIT 子句
聚集函数

- **查询指定列**

  ```sql
  #查询全体学生的学号与姓名
  SELECT Sno,Sname
  FROM Student;
  #查询全体学生的姓名学号专业
  SELECT Sname,Sno,Smajor
  FROM Student;
  ```

- **查询全部列**

  ```sql
  #1.把所有属性写出来
  SELECT Sno,Sname,Ssex,Sbirth,Sdept
  FROM Student;
  #2.*
  SELECT *
  FROM Student;
  ```

- SELECT 的目标列表达式可以是 **算术表达式、字符串常量、函数、列的别名**

- **查询经过计算的值**

  ```sql
  SELECT Sname,(extract(year from current_date) - extract(year from Sbirth))'年龄'
  FROM Student;
  ```

- 使用列别名改变查询结果的列标题

  ```sql
  SELECT Sname,'Date of Birth:',Sbrith,Smajor
  FROM Student;
  ```

  ![QQ图片20240414225714](E:/PS/08stu/QQ%E5%9B%BE%E7%89%8720240414225714.png)