## 数据类型转换

### 类型转换

#### 隐式类型转换

**不同数据类型的变量放一起运算时,数据类型转换自动发生.**
**低精度会自动转换为高精度再进行运算.**
**运算结果是高精度**

> int 和 char 相加, char 变量转换成 int 再与 int 相加,结果是int
>
> int 和 double 相加, int 变量转换成double 再与 double 相加,结果是double
>
> int+char+double=double

char类型转为int时,按ASCII码转换,example:

- '0'的ASCII是48,那么3+'0'=51;
- int a;a='A'+1,6 result_a=A的ASCII码值+1. (0.6丢失)

#### 显示类型转换

**用户自己处理**
**(目标类型)变量名**

> 如下文的 (double)b



### 数据丢失

**等式右边的数据类型会自动转换为左边的数据类型,类型转换可能导致数据丢失**

```
int a=2;
int b=5;
cout<<b/a; 2
cout<<(double)b/a; 2.5(b被强制转换为double,a自动转为double 结果是double 2.5)
int c=(double)b/a;
cout<<c; 2 double 赋值给 int c 数据丢失
```

## C++标准模板库(STL)

### swap,min,max

```
swap(a,b)
```

**交换两个变量的值**,无返回值
a,b可以是任何数据类型,但必须相同啊

> 不用定义第三个变量的情况下交换两个变量的值

```
max(a,b)
min(a,b)
```

返回比较出来的值,一次只能比两个

### vector

#### 定义

```
vector<typename> name; 定义一个vector
example:
vector<int> a{1,2,3}
vector<int> a={1,2,3}都可以
```

> typename 可以是任意基本类型: int char double 结构体...
> 也可以是STL的标准容器: vector,set,queue,stack....

这个相当于是一个**一维数组** name[size],只不过它长度可以根据需要变化,节省空间. 
把它当成数组用,可以通过下标访问与更新. 													

**基本类型**:			**examples**

```
vector<int> name;
vector<double> name;
vector<char> name;
vector<node> name;
```

**STL容器类型**:

```
vector<vector<int>空格> name;
vector<set<int> > name;
```



#### 迭代器

定义:

```
vector<typename>::iterator name;(name一般是it)
```

迭代器是一个类似指针的东西,可以用 * 解引用
可以通过 *it 访问 vector里的元素 
也可以用++,--来移动迭代器
两个迭代器相减的结果是 右侧迭代器向左移动多少个元素是左侧迭代器

#### 常用函数

```
使用方法:
name.函数()
```

|              函数名              |                   函数作用                    |
| :------------------------------: | :-------------------------------------------: |
|   v.c**lear ($\varnothing$)**    |                   **清空**                    |
|    **v.size($\varnothing$)**     |               **返回元素个数**                |
|    v**.front($\varnothing$)**    |                **返回首元素**                 |
|    v**.back($\varnothing$)**     |                **返回尾元素**                 |
|    v**.empty($\varnothing$)**    |     **判断是否为空,空返回true,非空false**     |
|      v**.push_back(elem)**       |            **在尾部添加元素elem**             |
|  v**.pop_back($\varnothing$)**   |               **删除尾部元素**                |
|    v**.begin($\varnothing$)**    |          **返回指向首元素的迭代器**           |
|     **v.end($\varnothing$)**     |      **返回指向尾部元素下一位的迭代器**       |
|         v**.erase(pos)**         |            **删除pos[^1]位置元素**            |
|     v**.erase(first,last)**      |         **删除[first,last)[^1]元素**          |
|     **v.insert(pos,n,elem)**     |          **在pos处插入n个elem[^2]**           |
| **v.insert(pos,first,last[^3])** | **在pos处插入另一个容器中[first,last)的元素** |

[^1]: 迭代器
[^2]: n可以不写,默认为0
[^3]: 另一个容器的迭代器

insert 和 erase 返回值都是pos位置的迭代器

#### 排序sort,reverse

```
sort(first,last,cmp)
reverse(first,last)
```

排序[first,last) 默认cmp a<b

**cmp**:自定义的比较函数

**reverse**: 将[first,last)元素反转





### stack

```
stack<typename> s;
```



|    **函数名**    |        **Function**         |
| :--------------: | :-------------------------: |
| **s.push(elem)** |      **元素else入栈**       |
|   **s.pop( )**   |      **移除栈顶元素**       |
|   **s.top( )**   |  **取得栈顶元素(不删除)**   |
|  **s.empty( )**  | **检测栈内是否为空,空为真** |
|  **s.size( )**   |    **返回栈内元素个数**     |

先进后出

### queue

```
queue<typename> q;
example:
queue<int> q
```



|      函数名      |         Function          |
| :--------------: | :-----------------------: |
|  **q.front( )**  |     **返回队首元素**      |
|  **q.back( )**   |     **返回队尾元素**      |
| **q.push(elem)** |   **尾部添加元素elem**    |
|   **q.pop( )**   |     **删除队首元素**      |
|  **q.size( )**   |     **返回元素个数**      |
|  **q.empty( )**  | **检测队列是否为空,空真** |

### map

类似**python**中的字典,一个key对应一个value

```
map<keytype,valuetype> mp;
example:
map< int , int > m{{1,2},{2,2},{3,2}};
```

> **map**特性:map会按照key的顺序从小到大排序,所以keytype必须可以比较大小

|         Name         |                Function                 |
| :------------------: | :-------------------------------------: |
|     mp.find(key)     | 返回key的迭代器it,不存在则返回mp.end( ) |
|     mp.erase(it)     |         删除it对应的key和value          |
|    mp.erase(key)     |            删除key和其value             |
| mp.erase(first,last) |            删除[first,last)             |
|      mp.size( )      |              返回元素个数               |
|     mp.clear( )      |              清空所有元素               |
|     mp.empty( )      |              判断是否为空               |
|     mp.begin( )      |             队首元素迭代器              |
|      mp.end( )       |               尾后迭代器                |
|    mp.count(key)     |   查看元素key是否存在[^count],是1否0    |

[^count]:  count统计个数,由于map中key只有一个,所以存在便是1,否则0

> mp.find[key] mp.count[key] mp[key] 都可以检查key是否存在,但是key不存在时,mp[key]会创建一个键值
> 最好用前两种,不增加空间负担

### string

```c++
string str1; //生成空字符串
string str2("123456789"); //生成"1234456789"的复制品 
string str3("12345", 0, 3 );//结果为"123" ，从0位置开始，长度为3
string str4("123456", 5 ); //结果为"12345" ，长度为5
string str5(5,'2'); //结果为"22222" ,构造5个字符'2'连接而成的字符串
string str6(str2,2); //结果为"3456789"，截取第三个元素（2对应第三位）到最后
```

|           Name            |              Function               |
| :-----------------------: | :---------------------------------: |
|   s.length()和s.size()    |            返回字符个数             |
|     s.push_back('a')      |           在尾部添加字符a           |
|   s.insert(pos,element)   |          在pos插入element           |
|       s.append(str)       |         在尾部添加字符串str         |
|       s.erase(pos)        |       删除迭代器pos所指的字符       |
|    s.erase(first,last)    |    删除迭代器[first,last)的字符     |
|     s.erase(pos,len)      |       从pos开始删除len个字符        |
|         s.clear()         |                清空                 |
|   s.replace(pos,n,str)    |    把从pos开始的n个字符替换为str    |
|   s.replace(pos,n,n1,c)   | 把从pos开始的n个字符替换为n1个字符c |
| s.replace(first,last,str) |    把[first,last)内字符替换为str    |
|       tolower(s[i])       |             转换为小写              |
|       toupper(s[i])       |             转换为大写              |

> strlen(char*)只能用于求 C中的 char 数组,同样的 s.size() 和 s.length() 不能用于 字符数组

#### 支持比较运算符

**>,>=,<,<=,==,!=**
大于小于号逐个字符比较,知道比较出大小

> str1 abcdefffff
> str2 abcdfeeee 
> abcd一样大,第五位f>e,结果是str2>str1

**+** 拼接字符串

```c++
string str1 = "123";
string str2 = "456";
string s = str1 + str2;
cout << s; //123456
```



## Lambda 表达式(失败)

又叫 **lambda** 函数,匿名函数

```
[capture list]	(parameters)	opt -> returntype {statement;};
	捕获列表	  参数列表			选项	  返回类型		函数体
```

捕获列表：捕获上下文的变量供Lambda函数使用,包含局部变量,捕获的变量可以直接在Lambda中使用
参数列表:  就是参数列表,跟普通函数一样,不需要时可以连同括号一起省略
返回类型:  返回值的类型,在结果明确时,可以不写:如结果明显是int,可以不写int,让编译器猜
				   不要返回值时 ->returntype可以省略,把->returntype看成一体就行
函数体:  不仅可以使用参数列表的参数,还能用捕获列表的参数

最简单的lambda表达式是: **[]{};** 可以通过编译,但是没任何作用

| 捕获列表形式 |           作用           |
| :----------: | :----------------------: |
|     [ ]      |        不捕获变量        |
|    [var]     |   值传递捕获的变量var    |
|     [=]      | 值传递所有父作用域的变量 |
|    [&var]    |     引用传递变量var      |
|     [&]      |  引用传递父作用域的变量  |
|    [x,&y]    |    x值传递,y引用传递     |
|     ...      |           ...            |

不能重复捕获 如 [=,x] =已经捕获x了,不允许再次捕获x

```c++
auto function = []{
	cout << "Hello World!" << endl;
};
傻逼编译器
```

> 为什么必须用auto? 
> 上面一直使用auto关键字来自动推导lambda表达式的类型，那作为强类型语言的c++，这个lambda表达式到底是什么类型呢？lambda的表达式类型在c++11中被称为『闭包类型(Closure Tyep)』，是一个特殊的、匿名的、非联合(union)、非聚合(aggregate)的类类型。可以认为它是一个带有operator()的类，即防函数(functor)。因此可以使用std::function 和std::bind来存储和操作lambda表达式。
> 原文链接：https://blog.csdn.net/bandaoyu/article/details/107390235

这段代码报错的原因是在使用auto关键字时，lambda表达式中使用了x++，而auto关键字默认推导为const类型，无法修改const类型的变量。因此，x++会导致编译错误。

如果你想要在lambda表达式中修改x的值，可以将auto关键字改为mutable，即将lambda表达式定义为可变的。修改后的代码如下：

```
cpp#include <iostream>
using namespace std;
int main()
{
    int x=100;
    auto func = [x]() mutable {return x++;};
    cout<<func();
    return 0;
}
```

这样就可以正常运行了。



auto关键字默认推导为const类型，无法修改const类型的变量。什么意思？是x变成const类型了吗？谁是const类型？是返回值是const类型？还是lambda都是const类型

auto关键字在默认情况下会进行类型推导，但是如果初始化表达式是const类型的变量，那么auto推导的结果也会是const类型。这意味着使用auto声明的变量将无法修改。

在这种情况下，如果使用auto关键字声明一个变量x并初始化为const类型的变量，那么x将被推导为const类型，无法修改x的值。

例如： const int a = 10; auto x = a; // x被推导为const int类型，无法修改x的值

在lambda表达式中，如果使用auto关键字声明一个变量并初始化为lambda函数，那么该变量也会被推导为const类型。这是因为lambda函数默认是const的，即使没有显式指定。

例如： auto lambda = { … }; // lambda被推导为const类型

所以，无论是使用auto关键字声明一个变量并初始化为const类型的变量，还是将lambda函数赋值给auto声明的变量，都会导致该变量被推导为const类型。

## for循环

for循环中三个表达式均可以省略,但是分号不能省略

```
for( 初始化; 判断条件; 控制条件)
```

- 初始化不写,表示不对循环变量赋初值
- 条件不写,一直循环                    for(; ;) = while(true)
- 控制条件不写,不控制循环变量

