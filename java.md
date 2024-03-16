## 规范

### 命名:
所有 **包/类/接口/方法/参数/变量** 的命名必须使用 
有意义且无歧义的 英文单词或其缩写
禁止中文,拼音以及中英混合

---

#### 类 命名:

驼峰式命名,每个单词仅首字母大写,其余小写
一般是单数,工具类可以用复数

---

#### 包 命名:

使用全部小写的英文单数名词
package 声明包的路径名称
必须放在源文件的顶部,源文件的位置必须与包声明的路径相同

---

#### 变量 命名:

首个单词的首字母小写,其余单词首字母大写

> string userName = "Petter"

---

#### 合法的标识符:

首字符仅支持26个字母和符号 $ , _ 不支持数字以及其他符号
后续字符可以是字母,数字以及 _ 不支持其他字符
但是为了规范: 不用 \$ 与 _ 开头

> \$count _count count\$ count_\$ 合法但是不要用

---

#### 数字字面量:
支持用下划线 _ 分隔,提高代码可读性
编译时会把 _ 忽略

> creditCardNumber = 1234_567_89

---

#### 常量 :
所有字母大写且用 _ 分隔单词 
final

> final int NUM_GEAR = 6

### long,double,float

#### long

长整型 long 的数值要以 L 结尾 

> long creditCardNumber = 12344456L
> long num = 123L
>
> 不用 L 结尾也不会报错,但是要规范,得加上

#### float

float 以 f/F 结尾,必须以 f/F 结尾

>  float num=1.23F

#### double

double 以 d/D 结尾,也可以不要
默认的double  类型允许不声明后缀

> double num = 1.23
> dounle num = 1.23D

---

## 函数

### switch

匹配到case中表达式时,执行代码 且顺次执行之后的所有case的代码块直到遇到break
也就是 没有break 它会一直进行下去

```
switch(num){
case 1:
	代码1
case 2:
	代码2
case 3:
	代码3
	break;
case 4:
	代码4
}
```

给num传入一个值,case 1: ->如果 num == 1 则执行该case的代码块
由于该case没有break,程序会接着执行case 2 和 case 3 直到case 3的break switch才结束
