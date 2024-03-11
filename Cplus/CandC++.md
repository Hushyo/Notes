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

### vector

#### 定义

```
vector<typename> name; 定义一个vector
```

> typename 可以是任意基本类型: int char double 结构体...
> 也可以是STL的标准容器: vector,set,queue,stack....

这个相当于是一个一维数组 name[size],只不过它长度可以根据需要变化,节省空间. 
把它当成数组用,可以通过下标访问与更新. 													

```
基本类型:			examples
vector<int> name;
vector<double> name;
vector<char> name;
vector<node> name;
STL容器类型:
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

#### 常用函数

```
使用方法:
name.函数()
```

|            函数名            |                 函数作用                  |
| :--------------------------: | :---------------------------------------: |
|    .clear ($\varnothing$)    |                   清空                    |
|     .size($\varnothing$)     |               返回元素个数                |
|    .front($\varnothing$)     |                返回首元素                 |
|     .back($\varnothing$)     |                返回尾元素                 |
|    .empty($\varnothing$)     |     判断是否为空,空返回true,非空false     |
|       .push_back(elem)       |            在尾部添加元素elem             |
| .pop_back(**$\varnothing$**) |               删除尾部元素                |
|    .begin($\varnothing$)     |          返回指向首元素的迭代器           |
|     .end($\varnothing$)      |      返回指向尾部元素下一位的迭代器       |
|         .erase(pos)          |            删除pos[^1]位置元素            |
|      .erase(first,last)      |         删除[first,last)[^1]元素          |
|     .insert(pos,n,elem)      |          在pos处插入n个elem[^2]           |
| .insert(pos,first,last[^3])  | 在pos处插入另一个容器中[first,last)的元素 |

[^1]: 迭代器
[^2]: n可以不写,默认为0
[^3]: 另一个容器的迭代器

