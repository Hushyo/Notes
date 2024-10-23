# Html

## 概述

idea中输入 c  直接tab 快捷注释  仅限于web文档
html标签不分大小写，建议全部小写

每个标签，从标签开始到标签结束是一个元素

每个元素**包括但非必须**的组成:
1.元素开始标签
2.元素开始标签中的属性
3.元素的内容
4.元素结束标签

属性以键值对的形式声明 如 name="value"
属性名称不分大小写，同样建议小写
属性值建议包括在双引号内，如果属性值本身带有双引号，可以把属性值的双引号改为单引号
\<a href="#"> 这是元素内容\</a>
开始标签   href 属性             结束标签

标签由<>包裹，所以元素内容里不能直接写<>
元素内容里  &lt 代表 <；$gt 代表>; &amp代表&

## 标签

*标签种类繁多，随用随加*

### 基础标签

***\<body>***该标签里面就是我们看到的内容

**\<h1~6>**一到六级标题
**\<br>**换行
**\<hr>**水平分割线

**\<!--注释-->**

两种段落

- \<p>
  内部的多个连续的回车或者空格都按一个来算

- \<pre>
  另一种段落,内部的连续多个空格/回车 按原样算



### 文档结构标签

HTML5新增的文档结构标签，本身并不带有特定的样式。
这些标签是为了更好地定义文档的结构和语义，便于开发者和搜索引擎理解页面的布局和内容。
增加可读性

| 标签名称    | 含义         |
| ----------- | ------------ |
| `<header>`  | 页眉         |
| `<nav>`     | 导航栏       |
| `<section>` | 节，定义段落 |
| `<article>` | 文章         |
| `<aside>`   | 侧边栏       |
| `<footer>`  | 页脚         |

### 文本标签

1. 斜体字标签
   `<i> 和 <em>`
2. 粗体字标签
   `<b> 和 <strong>`
3. 上标标签 和 下标标签
   `<sup> 和 <sub>`
   \<sup> **^上标^** \<sub> **~下标~**
4. 修订标签
   `<del> 和 <ins>`
   ~~修订标签~~
5. 预格式化标签
   `<pre> `里面是什么就输出什么，不管你有多少空格回车

### 列表标签

1. 无序列表
   `<ul>`

2. 有序列表
   `<ol`

   两者标签里的项元素都用`<li>`标签包括

3. 定义列表
   `<dl>`
   内部元素项由`<dt>`和`<dd>`组成

   ```
   <dl>
       <dt>第一项标题</dt>
       <dd>第一项定义</dd>
       <dt>第二项标题</dt>
       <dd>第二项定义</dd>
   </dl>
   ```

​		<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240918181011026.png" alt="image-20240918181011026" style="zoom: 50%;" /> 

### 图像标签

`<img>`

常用属性 `src` 属性 和 `alt` 属性
`src` 图片资源的地址，来源，这个地址有效时才会显示图片，无效则显示alt内容
`alt` 图片不能正常加载时对外显示的内容

其他常见属性

1. title 属性
   鼠标悬浮在图片上时提示的内容
2. width/height
   设置图片的大小，图片大或小时会自动充满这个大小（可能失去纵横比）
3. object-fit
   与4结合起来用，代表图片充满大小时的缩放方式
   - fill 默认值 图片自动缩放至填满容器
   - contain 等比例缩放，直到图片完全进入容器
   - cover 等比例缩放至图片某一边完全填充容器

关于图像的布局，我们可以在HTML中调整图像的大小
最简单的方法之一是直接调整 img 元素的 width/height 属性
比如一个 640x960 的图片 我们可以设置它的宽高为 400x500

在我们设置了图片的大小后，如果图像实际尺寸跟我们设计的尺寸不匹配，浏览器会缩小或者放大图像
浏览器调整大小难免出现图片质量差的问题，所以我们应该把调整好的图片放到网页里
调整图片可以使用 Thumbor 或者免费图像CDN如ImageKit.io

#### **图片大小**

1. 直接在css中调整图像大小，即手动设置图片大小

   ```
   img{
   width:400px;
   height:300px;
   }
   ```

2. 调整图像大小时保留纵横比
   高宽设置一个，另一个设置auto

   ```
   img{
   width:400px;
   height:auto;
   }
   ```

3. 根据可用宽度调整图像
   其一：

   ```
   img{
   width:100%;
   height:auto;
   }
   ```

   其二： 使用max-width/height属性
   在这种情况下，如果必须，图像会缩小，但是永远放大到大于其实际尺寸

   ```
   img{
   nax-width:100%;
   height:auto;
   }
   ```

**如何调整大小和裁剪图片以适合元素区域**
到目前为止，我们已经讨论了如何通过指定调整图像大小 width/height
当我们同时指定两者时，图片将被强制适应所要求的尺寸，它会改变纵横比来适应尺寸。
有时我们宁愿图像部分裁剪，也不愿失去纵横比
为此，我们可以使用
1.把图片作为背景图插入;2.设置img的object-fit属性

1. background-image
   图像作为背景插入，图像作为背景插入时，不会溢出容器，容器有多大，他就显示多少
   ![image-20240701150332744](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240701150332744.png)

   常用的导入方法是 url("path")-> background-image:url("path")

   当图片作为 background-image插入时，我们通过以下css属性控制其尺寸

   - background-size 图像的大小
     跟img直接设置宽高效果一样，不过该属性仅作用于背景image，而前者仅作用于img
     默认情况下图片以实际尺寸显示
     background-size的可能值:

     1. auto  以实际尺寸渲染图像

     2. 具体值 如 100px;  100px 100px;  100%;
        只有一个值的时候，另一个值默认 auto，保持纵横比

        ```
        div.img{
                    background-image: url("resource/img/cat.png");
                    background-size: 100px;
                    width: 320px;
                    height: 180px;
                }
        ```

        ![image-20240701150637169](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240701150637169.png)
        不设置 background-repeat:no-repeat是这样的

     3. contain
        保持纵横比调整图片大小直至整个图片完全可见，所以可能出现占不满的情况(比如宽已经完全进去了，但是高还没，还得继续缩小，继续缩小导致完全进去时宽不够了)

     4. cover
        保持纵横比缩小直到图像的一边完全进入容器

   - background-position 背景图像的起始位置

2. object-fit
    指定在设置 img 的 width/height 时图片会被如何缩放
   这个属性要定义在 img 上，与 img 的 width/heigth 同时使用
   使用 width/height 指明图片要变成多大，object-fit 指明图片怎样放缩

   - fill  默认值 图片将完全填满img设置的大小，意味着失去纵横比
   - contain  图片完全放入
   - cover 图片直至某一边放入
   - none 图片以原尺寸拿下来一块儿塞进去

---

### 超链接标签

`<a>`超链接，里面的内容会变成可以点击的连接，可以放入任何内容，包括图片

1. href  属性 
   跳转地址，相对绝对都可以
   地址开头没有 / 就是相对地址

   如果页面里由某个元素声明了id,那么href="#id" 这个链接就会跳转到这个元素的位置，**也就是锚点**

2. target 属性
   目标内容打开方式

   | target属性值 | 打开方式   |
   | ------------ | ---------- |
   | _self        | 原窗口打开 |
   | _blank       | 新窗口     |
   | _top         | 顶层框架   |
   | _parent      | 父框架     |

3. **超链接的颜色**
   如果在层层容器下写了一个 超链接 \<a>
   <font color=red>待补充</font>

### 表格标签

`<table>`

<font color=green>有几个标签是用在表格里的
\<thead> 代表表格的标题，头部
\<tbody> 代表表格的主题
\<tfoot> 代表表格的脚
这三者只是用来区分，并无实际效果</font>

#### 表格组成

1. 表格行标签
   `<tr>`
2. 单元格标签
   `<td>` 
3. 表头标签
   `<th>`
4. 表格标题标签
   `<caption>`

```html
<table>
    <caption>表格标题</caption>
    <tr>
        <th>1</th>
        <th>2</th>
        <th>3</th>
    </tr>
    <tr>
        <td>1.1</td>
        <td>2.1</td>
        <td>3.1</td>
    </tr>
</table>
```

th只是处于第一行的td，只是多了自动加粗和居中而已
单元格标签放在行标签里，表格才能换行，不然就是一行排开

`<tr>`标签中只能嵌套`<td>`标签，不能在其中输入文字

#### 表格属性

|    属性     |               描述                |
| :---------: | :-------------------------------: |
|   border    |        表格边框宽度，默认0        |
| cellspacing | 单元格与单元格之间的空间，默认2px |
| cellpadding |       单元格内边距，默认1px       |
|    width    |             表格宽度              |
|   heigth    |             表格高度              |
|    align    |     与其他同级元素的对齐方式      |
| background  |           表格背景图像            |
|   bgcolor   |           表格背景颜色            |

border-collapse: collapse; 可以让边线合并

### 框架标签

`<iframe>`
HTML5只保留了内联框架标签`<iframe>`
仅支持`src`属性,指定框架内部网页来源
就是把另一个网页插入到该网页里，可以使用里面的网页

```
<iframe src="https://www.bilibili.com/"></iframe>
```

但是这个框架默认尺寸太小了，最好手动设置一下

### 进度标签

1. 记号标签
   `<mark>`
   用于==突出显示==指定区域的文本内容,高光

2. 进度标签 
   `<progress>`
   用于显示任务的进度，生成一个进度条，进度的内容由max,value决定

   ```html
   10/100  <progress value="10" max="100">这里不用内容</progress>
   ```

   <img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240918184137215.png" alt="image-20240918184137215" style="zoom:33%;" /> progress标签内不用写任何内容，写了也不显示

3. 量度标签
   `<meter>`
   用于显示标量测量结果，如投票数据统计
   这个属性就多了

   | 属性名称 | 解释                                                   |
   | :------: | ------------------------------------------------------ |
   |  value   | 实际数值,可以整数可以小数 默认0                        |
   |   min    | 规定最小值，不可小于0 默认0                            |
   |   max    | 规定最大值，不可小于min 默认1                          |
   |   low    | 规定较低值，value低于这个值显示红色                    |
   |   high   | 规定较高值，value 在[low,high]之间黄色，高于high为绿色 |
   | optimum  | 规定最佳值，必须在 [min,max]之间                       |

   ```html
   磁盘:25/100<meter min="0" max="100" value="25" low="30" high="60"></meter>	
   ```

   <img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240918185730164.png" alt="image-20240918185730164" style="zoom:50%;" /> 

   不能用CSS设置其属性

   ```
       <style>
           meter.low{
               min: 0;
               max: 100;
               low: 30;
               high: 60;
               value: 25;
           }
       </style>
       这样是无效的，只能直接在它里面设置，奇怪
   ```

## 表单标签

`<form>`
收集用户数据并传递给后台服务器，实现网页与用户间的沟通对话

表单由 **表单域，表单控件，提示信息**构成
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240918190939627.png" alt="image-20240918190939627" style="zoom:50%;" /> 

表单域就是一个容器
提示信息是说明性的文字
表单控件就是具体的功能项，比如输入框，单选框······



`<form> </form>`定义一个完整的表单框架，内部可以包含各式各样的表单组件
具有以下属性

1.  action 属性
   代表表单将要传到哪里，规定表单提交数据的服务器地址
   值为URL地址，表单提交后会带着表单跳转到action里URL地址
   如果给form绑定一个事件，事件返回值是false时便不会跳转
   
2. method 属性
   规定发送表单的HTTP方式，是get请求还是post请求啊

   - get 默认值，代表表单上传时发出get类型请求
   - post  上传发出 post 类型请求

3. enctype 属性
   决定表单发送时使用的编码类型
   - application/x-www-form-urlencoded 编码所有字符
   - multipart/form-data 不对字符编码，当表单有上传文件功能时必须用这个
   - text/plain 不对特殊字符编码

4. name 属性
   规定表单的名称，具有唯一性 

5. target  属性
   服务器响应的打开方式，点击提交后，如果服务器有响应，这个值决定了这个响应打开的方式

   |     值     |    解释    |
   | :--------: | :--------: |
   |   _self    | 本页面打开 |
   |   _blank   |  新开页面  |
   |  _parent   |   父容器   |
   |    _top    |  顶层容器  |
   | iframename |  内联框架  |

### 输入标签

输入标签
\<input type="输入类型" name="自定义名称" />
type属性代表输入类型，type类型如下

| 类型名         | 解释                    |
| :------------- | ----------------------- |
| text           | 单行文本输入框          |
| password       | 密码输入框，字符被*替换 |
| radio          | 单选框                  |
| checkbox       | 复选框                  |
| submit         | 提交按钮                |
| reset          | 重置按钮                |
| button         | 单纯的按钮              |
| image          | 图片形式的提交按钮      |
| file           | 提交文件                |
| hidden         | 隐藏输入字段            |
| date           | 日期选择框              |
| datetime-local | 日期加时间选择框        |
| number         | 数字选择框              |

password 输入内容变成星号*

checkbox
输入框摇身一变变成复选框![image-20240629145152343](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629145152343.png)

radio
输入框摇身一变变成单选框
多个单选框用 name属性分组，name属性值相同的为一组
同一组单选框只能选择一个

file
将输入框变成`上传文件`选项
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629145631619.png" alt="image-20240629145631619" style="zoom:67%;" />

hidden
不会渲染在页面里，看不到，但是可以正常提交
多用于不需要看但是需要用的值

date
变成选择时间的框
![image-20240629145942097](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629145942097.png)

datetime-local
在上述基础上可以选择当天时间
![image-20240629150016307](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629150016307.png)

number
选择数字的框
![image-20240629150108745](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629150108745.png)
可以直接输入，也可以点右边的上下箭头增加/减少



**其他属性**

| 属性        | 属性值   | 效果                         |
| ----------- | -------- | ---------------------------- |
| name        | 用户定义 | 控件名称                     |
| value       | 用户定义 | 控件中文本默认值             |
| placeholder | 用户定义 | 控件中提示性文本，不会被提交 |
| size        | 正整数   | 控件宽度                     |
| readonly    | readonly | 只读，不能编辑               |
| disabled    | disabled | 初始禁用该控件，显示灰色     |
| required    | required | 控件填写后才能提交表单       |
| checked     | checked  | 默认选中控件                 |
| maxlength   | 正整数   | 允许最多输入的字符数         |

1. placeholder 
   该属性的值作为文本未输入时显示的内容，作为提醒
   ![image-20240629144436820](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629144436820.png)
2. checked
   配合 type="checkbox" 使用
   如果该属性为 true 那么该复选款便是选中状态
3. accept
   配合 type="file" 使用
   该属性为用户提醒上传文件的类型
   但是并没有限制文件类型
   ![image-20240629145817315](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629145817315.png)
4. min/max

   - 配合type=date或者另一种date时
     代表可选时间范围
     \<input type="date" min="2024-04-09">
     但是这个值必须是 yyyy-mm-dd 形式的，单数月/日用0补齐
   - 配合 type=number 使用时代表数字最大最小值
5. required
   同样是写上就起作用
   该输入框填写完毕后表单才可以提交
   不然会提醒用户填写表单
6. disabled
   写上就起作用
   :不可用
   不允许修改，提交也不带他
7. list
   值为 \<datalist> 标签的  原生 id
   作为一个下拉可选可输入的菜单,不像select一样只能选

### 多行文本标签

type=text只是一个单行输入框，现在引入多行输入框 
`<textarea>` 这个元素允许文本回车换行，也叫输入域
可选属性项

```html
<textarea cols="每行字符数" rows="显示的行数"> 文本内容 </textarea>
```

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629145000891.png" alt="image-20240629145000891" style="zoom:67%;" /> 

### 表记标签

`<label>`

可放置在`<input>`前后为其定义表记，通常为文本形式，作为其的补充说明
显示效果与普通文本一致，但是被点击时，对应控件也会生成焦点，相当于也被点击一次

在`<label>`元素的==首标签==中使用==for==属性引用对应控件的 ==id==名称
直接接收id 而不是#id

```html
<label for="name">姓名</label>
<input type="text" id="name"/>
```

也可以直接用该元素的首尾标签包围对应控件，无序设置id
这样元素内容就直接连接到元素上，不用再声明 for 属性了

```html
<label>姓名 <input type="text" id="name"/></label>
```

两种使用方法效果完全相同

### 列表标签

`<select> </select>`

添加一个下拉菜单选择框
里面至少要有一对 `<option>`
select的四个属性

| 属性名   | 属性值     | 效果                                           |
| -------- | ---------- | ---------------------------------------------- |
| disabled | disabled   | 禁用列表菜单                                   |
| multiple | multiple   | 允许同时选中多个选项<br />用户按住ctrl可以多选 |
| name     | 自定义名称 | 规定列表元素的名称                             |
| size     | 数值       | 规定列表菜单红可见选项的个数                   |

size 默认应该是1，一眼只能看到一个选项

**\<option>**
选项元素
下拉菜单默认显示代码里的第一个 \<option>
所以想要下拉菜单默认是空的话，第一个\<option>元素设置空

value属性值是表单提交过去时，该select菜单传过去的值
想要某一项默认选中，应该再加上 selected属性 ，而不是checked

```
<select>
    <option value=""></option>
    <option value="">1</option>
    <option value="">2</option>
    <option value="">3</option>
</select>
```

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629150531271.png" alt="image-20240629150531271" style="zoom:50%;" /> 



**\<optgroup>**
为option分组，内部 label属性代表组名
该开始标签和结束标签内的 option 为一组

```
<select>
    <option value=""></option>
    <optgroup label="number">
    <option value="">1</option>
    <option value="">2</option>
    <option value="">3</option>
    </optgroup>
    <optgroup label="alphabet">
        <option value="">a</option>
        <option value="">b</option>
        <option value="">c</option>
    </optgroup>
</select>
```

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629150833306.png" alt="image-20240629150833306" style="zoom:50%;" /> 

**\<datalist>**
声明 id 属性，为type=list的input提供下拉后的选项

内部同样可以放很多 \<option> 元素
作为下拉菜单的可选项

### 按钮标签

`<button>`

| 属性名   | 属性值                        | 效果                                               |
| -------- | ----------------------------- | -------------------------------------------------- |
| disabled | disabled                      | 禁用当前元素                                       |
| name     | 自定义                        | 规定按钮名称                                       |
| type     | button<br />submit<br />reset | 规定按钮类型                                       |
| value    | 文本                          | 规定按钮初始值<br />按钮中文本是首尾标签中间的内容 |

### 域标签

`<fieldset> </fieldset>`
以及域标题标签 `<legend></legend>` 

基本用法

```html
   <fieldset>
       <legend>域标题</legend>
       控件1 <input type="text"><br>
       控件2 <input type="text">
	   控件n
   </fieldset>
```

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240919162027338.png" alt="image-20240919162027338" style="zoom:80%;" /> 



## 多媒体

### 概述

**视频，音频嵌入技术**

运用HTML5中新增的 `<video>`标签和 `<audio>`标签来嵌入视频或音频

但是在不同浏览器上渲染出来效果也各不相同

**支持的格式**

HTML5支持的视频格式和音频格式
视频格式：ogg , mp4 , Webm
音频格式：ogg , mp3 , wav



### 使用

#### 视频

在HTML5中，用`<video>`标签定义视频文件

```html
<video src="资源URL" controls="controls">可插入文字</video>
```

src设置视频路径，controls控制是否显示播放控件 ， 文字会在浏览器不支持该标签时显示
视频的宽高也可以用CSS来设置，虽然在页面内看起来大小变了，但是视频的原始大小没变
实际工作应该用视频处理软件对视频进行压缩

其他属性

| 属性     | 属性值                   | 效果                                                         |
| :------- | ------------------------ | ------------------------------------------------------------ |
| autoplay | autoplay                 | 页面载入后自动播放                                           |
| loop     | loop                     | 视频结束重新播放                                             |
| preload  | auto<br />meta<br />none | 出现该属性，则视频在页面加载时加载<br />并预备播放，如果有autoplay，则忽略该属性 |
| poster   | url                      | 视频缓冲不足时，该属性值链接一个图像<br />视频会显示这个图像 |

chrome在2018年1月取消了自动播放功能，即autoplay属性失效。我们想要自动播放需要为 video 标签添加 muted 属性，使其静音播放

```html
<video src="" muted=false defaultMuted=false controls> </video>
```

| 属性         |                             |
| ------------ | --------------------------- |
| muted        | 设置或返回音频/视频是否静音 |
| defaultMuted | 设置或返回音频/视频是否静音 |

两者属性值都有true/false
true:静音
false:不静音

---



#### 音频

在HTML5中，`<audio></audio>`标签用于定义音频文件

```html
<audio src="资源URL" controls>可插入文字</audio>
```

controls同样是播放控件

| 属性     | 属性值                   | 效果                                                         |
| :------- | ------------------------ | ------------------------------------------------------------ |
| autoplay | autoplay                 | 页面载入后自动播放                                           |
| loop     | loop                     | 视频结束重新播放                                             |
| preload  | auto<br />meta<br />none | 出现该属性，则视频在页面加载时加载<br />并预备播放，如果有autoplay，则忽略该属性 |

### 兼容性

HTML5支持的视频音频格式，浏览器不一定支持
所以我们嵌入视频音频时，要考虑到浏览器的兼容性

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240919163600277.png" alt="image-20240919163600277" style="zoom:80%;" /> 

为了防止浏览器不兼容
现在引入了`<source>`标签，该标签可以为以上两种标签提供多个备用文件
该标签没有尾标签

```html
<audio controls>
    <source scr="URL" type="媒体文件类型/格式">
    <source scr="URL" type="媒体文件类型/格式">
    <source scr="URL" type="媒体文件类型/格式">
    <source scr="URL" type="媒体文件类型/格式">
</audio>
```

src指定来源
type指定插入文件的类型和格式 如果是音频 则写 audio 格式写音频的格式 如mp3

1. 

## 新增API



# Css



## 引入



### 样式表

1. **内联样式表**又称为行内样式表
   <元素名 style="属性名称:属性值">
   作用范围仅在该元素内部，优先级最高

   ```html
   <p color="red"> </p>
   ```

2. 内部样式表
   通常位于`<head> </head>`标签内部，用`<style> </style> `包围，作用范围为当前整个文档
   优先级第二

   ```html
   <style>
   p{
   color:red;
   }
   </style>
   ```

3. 外部样式表
   外部样式表为独立的CSS文件，后缀为.css或.CSS
   在`<head> </head>`中间使用 `<link>`标签引用，作用范围当前整个文档

   ```html
   <link rel="stylesheet" href="文件URL">	
   ```

   优先级最低



### 语法



**注释**
内部样式表和外部样式表文件中均可以使用 **`/*注释内容*/`** 这个格式进行注释



**@charset**
用在外部样式表里，用于指定当前样式表使用的字符编码
一般写在外部样式表文件的第一行，并且需要加上分号结束。

```
@charset "utf-8";
```



**!important**
表记CSS样式的使用优先级

```html
p{
background-color: red !important;
background-color: blue;
}
上述代码表示优先使用background-color: red语句，即段落元素的背景颜色设置为红色
```



### 单位 

#### 数字

数字有三种取值形式

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240921134534782.png" alt="image-20240921134534782" style="zoom:67%;" /> 

#### 长度

表示方法为 数值接长度单位
可用于描述文本 图像或其他各类元素的尺寸

长度取值单位可以分为相对长度单位和绝对长度单位

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240921134417151.png" alt="image-20240921134417151" style="zoom:67%;" /> 

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240921134430243.png" alt="image-20240921134430243" style="zoom:67%;" /> 

#### 角度

可用于描述元素变形时旋转的角度

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240921134604369.png" alt="image-20240921134604369" style="zoom:67%;" /> 

#### 时间

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240921134635543.png" alt="image-20240921134635543" style="zoom: 50%;" /> 

1. px 像素 绝对单位

2. em 相对单位 相对于当前元素的尺寸
   比如设置字体为30px，然后再次设置字体0.5em
   那么字体最终是15px

3. rem 相对于默认尺寸

4. %相对于父容器的尺寸

5. vh 高度单位，相对于窗口高度
   vw 宽度单位，相对于窗口宽度





## 选择器

### 通配符选择器

```
*{}
```



### 元素选择器

也叫标签选择器？

```
元素名{}
```



### id选择器

```
#id名{}
```



### 类选择器

```
.类名{}
```



### 交集选择器

交集选择器由两个选择器组成，两者之间不能有空格
类选择器和id选择器也能组合

```
#id.className{}  id与类组合
tag.className{} 元素选择器与类选择器组合
```



### 并集选择器

多个选择器用`逗号`隔开，这几个选择器共享样式

```
p,div,#id,.className{}
```



### 后代选择器

空格隔开

```
div p{}  div下的所有p元素
div p,div{} div下的所有 div和p元素
选择器套选择器
```

\>隔开

```
div>p{} div的直接子元素p
```



### **兄弟选择器**

**同级紧邻选择器**
+隔开

```
div+p{}与div元素同级且下方紧邻的第一个p
```

**同级选择器**
~隔开

```
div~p{}与div元素同级且在下方的所有p
```





### 属性选择器

属性选择器可以根据标签的 属性 及 属性值 来选择对应标签，从而为标签设置差异化的CSS样式
下面value的双引号要不要都行

**E[arrtibute]**

选取标签名称为E，并且定义了attribute属性的标签。
E可以省略，如果省略则表示可以匹配满足条件的任意标签

```
div[id] 选取声明了id属性的div元素
[id] 选取所有声明了id的元素
```



**E[attribute=value]**

选取标签名称为E，并且定义了attribute属性，该属性就是value属性值的标签，E也可以省略

```
div[align=center] 选取包含align属性且属性值只为center的div标签
[align=center]  选取所有包含align属性且属性值只为center的标签
```



**E[attribute~=value]**

选取标签名称为E，定义了attribute属性，该属性包含某个value属性值的标签
以 class属性举例，一个元素的class属性可以声明多个来完成叠加样式，而这多个里面只要含有 value ，该元素就能被选中

```
div[class~="red"]
<div class="red content">就能被选中
```



**E[attribute|=value]**

选取带有value属性值或以 value- 为前缀的属性值的元素 

```
img[alt|="flower"]
选中所有alt属性以flower-开头的img 元素
或者alt就等于flower的img元素

<img alt="flower">  可以
<img alt="flower-a"> 可以
<img alt="flowera">	 不行，这个flower是前缀
```



**E[attribute^=value]**

选择标签名称为E，并且定义了attribute属性，属性值**前缀**为value字符的标签

```
div[id^="section"]

<div id="section-a">
<div id="sectiona">
<div id="section">
三者都可以！
```



**E[attribute$=value]**

选择属性值后缀为value字符的标签

```
div[id$=section]

<div id="asection">
<div id="a-section">
<div id="section">
都可以！
```



**E[attribute\*=value]**

选择属性值包含value字符的标签

```
div[id*=a]

<div id="asd">
只要属性值字符串中包含value 就行
```



### 伪类选择器

选择元素的特殊选择器，它允许你在特定状态下选择元素
伪类不同于普通的CSS类选择器，它们用于选择元素的特定状态或位置，而不是选择具有特定类名的元素

伪类通常以 单个冒号:开头
伪元素以两个冒号 :: 开头

#### 结构化伪类

**:root选择器**
匹配文档的根标签，根标签指的是 `<html>`标签

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
</body>
</html>
```

因此使用:root对所有页面内的标签都生效



**:not选择器**

排除设置的标签或属性，或者说是选择不匹配某元素的标签；
通常用作交集选择器(我认为嗷)

```html
h3:not(.not)
选择没有类名not的h3标签
:not(.not)
选择没有类名not的所有标签
所以最好组合成为交集选择器
```



**:only-child选择器**

用来选择没有兄弟元素且没有子元素的元素，但它需要直接作用于那个元素上，而不是它的父元素

```
<div>
    <p>
        blue
    </p>
</div>

p:only-child 作用于这个p上
而不是用 div:only-child

<div>
    <p>blue
    <div>a</div>
    </p>
</div>
这样的p也用不了，因为它有子元素
```



**:first-child/last-child**

用于选择其父标签中的第一个子元素和最后一个子元素
同样直接作用于那个元素上，而不是它的父元素

```html
    <style>
        p:first-child{
            color:blue;
        }
    </style>
    <div>
    <p>1
    <div>a</div>
    </p>
    <p>2</p>
    <p>3</p>
	</div>
```

1变蓝,23不变，因为只有1是其父元素中的第一个子元素
而a也没变蓝，因为`p:first-child` 选择器只影响 `p` 标签，并不会影响嵌套在 `p` 标签内部的其他元素

**:nth-child(n)和:nth-last-child(n)**

first和last 只能选第一个和最后一个
现在引入这种选择器，可以选择第二个，第三个，倒数第二个第三个，或者是奇数个，偶数个

```
:nth-child(2) 选择其父标签中的第二个子元素
:nth-last-child(2) 选择其父标签中的倒数第二个子元素
```

**:first-of-type和:last-of-type**

用于选择其父标签中第一个/最后一个特定类型的子标签

**:nth-of-type(n)和:nth-last-of-type(n)**

用于选择其父标签中第n个/倒数第n个特定类型的子标签

**:empty**

选择没有子标签或者内容为空的容器
文字也算内容嗷

```html
<div>这是一个有内容的div</div>
<div></div>
<span>这是一个有内容的span</span>
<span></span>
div:empty {
    border: 2px solid red;
}
span:empty {
    background-color: yellow;
}
第二个div和第二个span会被选中
```

**:target**

用于选择当前活动的锚点目标元素
这通常与 URL 的锚点（hash）一起使用，当浏览器的地址栏中包含一个锚点，如 `#section1`，那么 `id` 为 `section1` 的元素就会被选中

```html
<div id="a">a</div>
<div id="b">b</div>
<a href="#a">a变色</a>
<a href="#b">b变色</a>
 :target{
            background:yellow;
        }
注意是锚点，点了之后对应id的元素就匹配上了
```



#### 状态化伪类

超链接的四种状态化伪类选择器

:link
未访问时的默认样式

:hover
鼠标悬浮在元素上时样式
a:hover{} a元素在鼠标悬浮时的样式

:visited
超链接被访问后的样式
a:visited{} 点击过的a元素的样式

:active
鼠标点击不动时

这四种选择器对排列顺序是有要求的
通常按照 a:link a:visited a:hover a:active顺序书写
否则定义的样式可能不管用

:focus
具有焦点时

:checked
元素被选中时的样式 

:disabled
禁用时

:enabled
启用时



#### 伪元素选择器

伪元素用单冒号兼容性更好，但是为了规范，最好用双冒号

**:before**

用于在被选取的标签前面插入内容，但是在使用该选择器时
必须定义content属性来指定要插入的具体内容

```
标签名:before
{
    content:文字/url();
    被插入的可以是文字也可以是图像
}
```

**:after**

用于在被选取的标签后面插入内容，用法与前者相同







## 显示类型

**display**属性
值：

1. block
   块级，高度根据内容决定，宽度能占多宽占多宽
2. inline
   内联级，跟别人连在一起
3. none
   不显示，也不占用空间
4. inline-block
   对外能连到一起，对内能容纳block级元素
5. flex

   声明后，该元素变成弹性容器，内部的直接子元素变为弹性项



## 边框/背景



### 边框

|    属性名     |     效果     |
| :-----------: | :----------: |
|    border     |   设置边框   |
| border-radius | 设置圆角边框 |
|  box-shadow   | 设置阴影边框 |
| border-image  | 设置图片边框 |



##### **圆角边框**

border-radius: length|percentage
length 使用长度规定边框圆角的半径
percentage使用百分比规定圆角半径
两者均不可为负值

```
p{border-radius:20px;}为p元素设置半径为20像素的圆角边框
```

圆角边框可以分别设置四个角

| 属性                       | 效果   |
| -------------------------- | ------ |
| border-raidus              | 四个角 |
| border-top-left-radius     | 左上角 |
| border-top-right-radius    | 右上角 |
| border-bottom-left-radius  | 左下角 |
| border-bottom-right-radius | 右下角 |

取值均可以是长度或者百分数



##### 阴影边框

为边框添加阴影，默认值为none,即无阴影效果

box-shadow: x,y,width,color
分别标识 x偏移值，y偏移值，羽化半径（阴影宽度），颜色
想要使用第三个参数，必须先指定前两个参数 1px 2px 3px; 
如果只有两个数字参数，那么第三个参数默认0

x>0 右偏移，x<0 左偏移



##### 图像边框

| 属性名              | 效果                                   |
| ------------------- | -------------------------------------- |
| border-image-source | 指定图像来源，默认none                 |
| border-image-slice  | 设置图片的分割方式                     |
| border-image-width  | 边框厚度                               |
| border-image-outset | 图片超出边框的量                       |
| border-image-repeat | 设置图片的平铺状态                     |
| border-image        | 复合属性，可以一次性定义边框的全部设置 |

1. **设置边框图像**：使用 `border-image-source` 属性来指定边框图像的路径。

2. **调整边框图像**：使用 `border-image-slice` 来定义图像的哪一部分用于边框。

3. **设置边框宽度**：使用 `border-image-width` 来定义边框的宽度。

4. **设置边框偏移**：使用 `border-image-outset` 来定义边框图像向外扩展的距离

   定义了width后才会出现边框

border-image-source值是图片的来源，应该写作 url("具体URL")  这种形式

border-image-slice 属性有三种取值 默认100%
number 数值规定宽度，可以是整数，浮点数，不能是负数
percentage 百分比规定宽度，不能是负数
fill 保留裁剪后的区域，这部分区域由 repeat规定

border-image-repeat有三种取值
 repeat 重复平铺方式填充边框，图片超出的部分会被截断
round 重复平铺填充，图片根据边框尺寸动态调整至刚好能铺满整个边框
stretch 拉伸图片方式填充边框，默认是这个

border-image是他们所有的简写模式 声明顺序如下
source,slice,width,outset,repeat
none 100% 1 0 stretch 这是他们的默认值，如果其中部分属性不写，则取默认值

如果同时设置了 border-style和 border-image 优先显示  border-image



### 背景

| 属性名            | 效果                   |
| ----------------- | ---------------------- |
| background-clip   | 定义背景图片的绘制区域 |
| background-origin | 定义背景图片的位置     |
| background-size   | 定义背景图片的尺寸     |



background-clip用于裁剪元素的背景图片或颜色区域，使其只显示指定的区域内容
background-clip有四种取值
padding-box:只保留元素内边距之内的背景，包括内边距
border-box：只保留元素边框之内的背景，包括边框
content-box：只保留元素内容区域的背景，这个是默认值
text：只保留前景内容的形状，其他区域去掉，想用这个取值必须把属性名称写成 -webkit-background-clip

background-origin属性用于裁剪元素的背景图片，必须与background-image配合使用，否则没有图片来源无法对图片定位
background-origin有三种取值
padding-box:从元素内边距开始显示图像，这是默认值
border-box：从元素边框开始显示图像
content-box:从元素内容区域开始显示图像

background-size用于定义背景图片的大小
background-size: bg-size[,bg-size];

bg-size有五种取值
length:长度值规定图片大小，不可负值
percentage:百分比规定图片大小，不可负值
auto：图片真实大小
cover：图片等比例缩放至完全覆盖容器，可能有部分图片超出容器
contain:图片等比例缩放到宽度或高度与容器一直，图片始终在容器中，不会超出容器

```
background-size:200px;图片宽200像素，高度等比例缩放
background-size:200px 300px 图片宽200，高300
```



## 文本/字体



### 文本

两种文本效果

| 属性名      | 效果           |
| ----------- | -------------- |
| text-shadow | 为文本添加阴影 |
| word-wrap   | 长单词强制换行 |

text-shadow与box-shadow用法一样

```
text-shadow:1px 2px 3px black;
```

word-wrap规定文本的换行规则

word-wrap: normal|break-word;

有两种取值
normal:默认值，只允许在断字点换行，如果单词较长则直接溢出不换行 无换行效果
break-word:文本在边界内换行，单词较长则直接断开强制换行

### 字体

CSS3中通过@font-face的规则，网页可以显示任何字体
语法规则如下

```html
@font-face{
font-family:"自定义字体名称";
src:url('url地址')[format(<string>)]
}
font-family的名称可以自定义，使用时使用这个名称即可
举例
@font-face{
font-family:'diyfont';
src:url('diyfont.ttf')format('turetype')
}
    
p{
    font-family:'diyfont'
    }
```



## 盒子

### 元素组成

BOX由若干非必要内容组成

1. margin 外边距 
2. border 边界
3. padding  内边距
4.  content 内容 
5. background 背景



- **border**

  1. border-style
     定义边框的样式，比如实线 border-style:solid(default)

  2. border-width
     定义四个方向边框的宽度
     支持单独定义某个方向的宽度，其他方向不定义就是没有边框
     有四种定义方法

     1. 一个参数

        border-width: 1px; 
        四个方向都是 1px

     2. 两个参数
        border-width：1px 2px;
        第一个参数代表上下
        第二个参数代表左右

     3. 三个参数
        border-width:1px 2px 3px
        第一个参数代表上
        第二个参数代表左右
        第三个参数代表下

     4. 四个参数
        border-width：1px 2px 3px 4px
        第一个参数代表上
        第二个参数代表右
        第三个参数代表下
        第四个参数代表左

     逆时针来的

  3. border-color
     字面意思，颜色

  4. border-radius:
      圆角程度 
     border-radius:2px;
     border-radius:5%;

- **padding**
  内边距，决定了内容到边线的距离
  本身没有颜色，它撑起内容的颜色由该元素的背景颜色决定
  内容距离左右边框的距离也可以单独定义
  跟边框一样的四种方式四种规则

- **margin**
  外边距，决定了元素边框到其他元素的距离
  本身也没有颜色，撑起来的空间颜色由外部背景颜色决定
  也支持单独定义，同样的四种方式

  在声明了元素的宽度后，把margin:auto可以使元素自动居中

  如果两个元素同时声明了外边距，那么两者垂直方向的距离为两者中最大的那个，而不是两个边距加起来

- **background**
  背景，有多个属性，都可以单独设置

  1. background-color
     定义背景颜色

  2. background-image
     定义背景图片，有三种取值
     1.background-image: url("地址")
     2.
     3.

  3. background-repeat
     控制图片的重复方式，如果只有一张小图占不满容器，可以让他重复
     四个值
     1.repeat 上下左右重复
     2.repeat-x 左右重复
     3.repeat-y上下重复
     4.no-repeat 不重复

     background-attachment
     background-position 先不看

### 盒子模式

width/height实际上是元素内容的宽高
但是元素实际占用空间还受到 margin/border/padding影响

现在有 **box-sizing** 属性帮助解决这个问题
该属性有两个值

1. content-box 默认值
   所有元素的该属性默认这个值，代表宽高给元素内容，就是上面引言的部分。还受其他影响，布局计算困难
2. border-box
   此时，width/height就不再是元素内容的高宽，而是border+padding+元素内容的高宽
   所以可以让margin=0,然后该元素的高宽就直接确定了，拉开间距用padding就行了,方便布局



## 对齐方式

1. vertical-align 属性
   声明本元素与其他平级 inline 元素的垂直对齐方式
   这是对自己使用的，不是父容器命令子元素的
   - baseline(default) 默认基于元素的内容基线对齐
   - center 中心对齐
   - top 顶部对齐



## position

1. static (default)
   默认值，无特殊定位方式
   因为是无特殊定位方式，所以说手动设置 top/left/right/bottom 也没用
2. relative
   相对于默认定位来说只是多了允许定位
   可以手动设置 top/left/right/bottom,不设置的话也没有特殊效果
3. absolute
   相对于所在多级容器中最近的一个声明了 非static position属性值的容器进行定位，没有则相对于body
   **无敌悬浮**，图层在其他之上，不参与页面的渲染
4. fixed
   相对于窗口定位
   **无敌悬浮**，不参与页面渲染计算'



## 变形/动画

### overflow

对于溢出容器部分的处理方式

1. hidden
   溢出的部分不显示
2. visible
   溢出的就溢出，溢出部分不截断，显示
3. scroll
   溢出部分截断，但是给你一个滚动条看溢出的内容
4. auto
   自动，基于内容长度决定给不给滚动条

### transition

transition动画又称为过渡动画，在指定时间内让元素从原始样式转变为新的样式

过渡，在给定时间内平滑改变属性值，一：指定属性值；二：指定时间

| 属性名                     | 解释                                     |
| -------------------------- | ---------------------------------------- |
| transition-property        | 指定对何种CSS属性渐变处理                |
| transition-duration        | 指定transition动画的时间                 |
| transition-timing-funciton | 指定transition动画的渐变速度，缺省值ease |
| transition-delay           | 指定transition动画的延迟时间，缺省值0s   |
| transition                 | 复合属性，一次性定义以上四个属性         |

transition-property属性三种取值
none:默认值
all：所有属性都渐变
**transition-property**：指定属性渐变，如果有多个属性，用逗号隔开

```
transition-poperty: width,height,background; 
```

**transition-duration**: 时间
用于指定渐变动画时长，时间越长变化越慢，单位为秒或者毫秒，如果是0则瞬间切换

```
transition-duration:0s
```



**transition-timing-function**
用于设置渐变速率
transition-timing-function: 速率值，常见有六种可以选择
linear：匀速
ease:均匀变慢
ease-in加速
ease-out减速
ease-in-out先加速后减速
cubic-bezier 使用贝塞尔函数自定义速度变化



**transition-delay**
设置渐变动画延迟播放时间
transition-delay:时间
毫秒或者秒，跟duration用法相同

**transition**
复合属性，可以快捷设置上述四个属性，常用顺序为
transition-property,transition-duration,transition-timing-function,transition-delay

```
可以一次性设置多个，用逗号隔开即可
transition:
background-color 10s ease-in 10s,
color 10s,
width 10s;
```

将要变换的元素声明该transition属性值，而不是元素变换结果声明transition

```
div.trans{
transition: width 2s;
}//表示该元素的 width 变化时在2s内变成

div.trans:hover{
transition: width 2s;
}不要声明在变化后的样式里，没有用
```


### transform

transform属性用于元素变形，可以实现对元素进行移动收缩旋转等2D动画效果

这是一个属性，用法
transform: 方法  如下
transform: translate(x,y);

| 方法名          | 效果                                                         |
| --------------- | ------------------------------------------------------------ |
| translate(x,y)  | 元素移动到指定位置                                           |
| rotate(degree)  | 元素顺时针旋转指定角度<br />负数则是逆时针旋转               |
| scale(x,y)      | 元素尺寸缩放至指定倍数<br />x指定宽度，y指定高<br />只有一个参数等比例 |
| skew(xdeg,ydeg) | 围绕x轴和y轴翻转元素<br />skew(20deg,10deg)横向倾斜20度，纵向倾斜10度 |
| matrix（）      | 矩阵，先不写                                                 |

translate
用于移动元素的位置    

- translate( x , y, z ) 
  两个参数，第一个是水平，第二个是垂直 第三个是？不常用；正数右下  负数左上；
  只写一个参数时，这个参数给了x，y是0

  ```
  transform: translate(100px,50px);
  水平右移100px，垂直下移50px；   
  transform: translate(100px);
  水平右移100px
  ```

- translateX(x) 水平

- translateY(y) 垂直

- translateZ(z) 可能是图层呢？

rotate
用于旋转元素的角度
同上有四种取值，第一种是后面三种合起来的简便写法

- rotate(x,y,z)
  正的是顺时针, x的转轴垂直于屏幕 y的转轴是屏幕的竖线，z的转轴我不好说
  也是只写一个时先给了x
- rotateX(x)
- rotateY(y)
- rotateZ(z)

scale
用于改变元素的尺寸（缩放）

- scale(x,y)
  分开设置水平，垂直方向缩放的比例
- scale(n)
  等比例缩放

### shadow

元素有两种shadow属性

1. text-shadow
   只给该元素的文本设置阴影
2. box-shadow
   给该元素的盒子设置阴影

两者阴影设置方式一样，以文本为例
text-shadow: 1px 2px 3px color;
第一个 x  偏移量  第二个 y 偏移量 第三个 羽化半径 第四个 阴影颜色

### float

元素只能左右，不能上下浮动

### flex

弹性布局，弹性项会随着窗口自动缩放，而不像写死的间距，窗口不够大就显示不出来
弹性布局从某个容器变为弹性容器开始

1. 元素 display属性声明为 flex 该元素变成弹性荣去，其直接子元素变为弹性项，子元素的子元素不受影响

2. 弹性项具有 inline-block的特性，但并不是弹性项的display是inline-block

### 弹性容器

弹性容器的属性，影响容器内部的弹性项

#### **flex-direction**

决定弹性容器的主轴方向，弹性项沿着主轴展开，因此决定弹性项的分布方式

- row 默认值 水平横向排列
- column 垂直纵向排列
- row-reverse
  column-reverse
  以上两者的反向

![image-20240701153947514](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240701153947514.png)

#### **flex-wrap**

决定当宽度不够时，弹性项是否换行

- no-wrap 默认值 不换行，窗口装不下会首先压缩弹性项的大小，压不动也不换行，没空间就跑到浏览器外面看不到
- wrap 换行

#### **justify-content**

决定弹性项在主轴的对齐方式

- flex-start
- flex-end
- center
- space-between
- space-around
- space-evenly

![image-20240701154104576](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240701154104576.png)

#### **align-items**

决定子元素在交叉轴(主轴为横向，交叉轴便是纵向)上的对齐方式

- flex-start 顶着交叉轴开始
- flex-end  顶着交叉轴结尾
- center    在交叉轴中间
- stretch   填满交叉轴
- baseline  根据内容基线对齐

![image-20240701154302639](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240701154302639.png)

#### **gap**

设置容器内项目之间的**间距**，只控制项目与项目的间距，**对项目与容器的间距不生效**
有四种设置方式，跟上面设置padding,margin一样 一个值代表上下左右，两个值 第一个代表上下，第二个代表左右···
![image-20240701154650075](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240701154650075.png)

#### **align-content**

当容器内有多行时，`align-content` 定义多行的对齐方式

取值跟 align-items一样

![image-20240701154758159](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240701154758159.png)

### 弹性项

#### flex-grow

**在容器主轴上存在剩余空间时, flex-grow才有意义**
定义的是可**放大**的能力，`0` （默认）禁止放大，大于 `0` 时按占的比重分放大，负数无效
如果有多个弹性项同时声明 flex-grow:1 那么它们把剩下的平均分，这个数字就是分配剩余空间的比重

#### flex-shrink

**当容器主轴 “空间不足” 且 “禁止换行” 时, flex-shrink才有意义**
定义的是可**缩小**的能力，`1` （默认）等大于 `0` 的按比例权重收缩， `0` 为禁止收缩，负数无效
当窗口缩小时被压缩的比重

#### flex-basis

flex-basis指定了 flex元素在主轴方向上的初始尺寸,它可以是长度（例如 `20%` 、 `5rem `等）或关键字。
`felx-wrap`根据它计算是否换行，默认值为 `auto` ，即项目的本来大小。它会覆盖原本的`width` 或 `height`

#### align-self

之前弹性项在交叉轴的对齐方式都是由容器决定的，这个属性给了弹性项自己决定的权力
同样是那6个值 flex-start,flex-end,center ···





### 网页设计

网页设计弹性布局
由一个整体容器铺满全屏，然后这个容器变成弹性容器，里面塞满弹性项
铺满全屏  width:100% height:100%
我们缩小窗口时，所有都跟着缩小；当我们想让部分元素在窗口不够时宁愿跑到窗口外面不显示时应该怎么做呢？
设置这个元素 flex-shrink:0 明显不好使，为什么呢？因为整体容器的宽高设置的是100%，容器是跟着窗口变大变小的，对于容器里面的元素来说也只是跟着各自的父容器变大变小罢了，根本就没有涉及到 shrink的压缩，所以不好使
问题根源 在于整体的容器，我们希望整体的容器在不够时跑到外面，但是又不能不设置100%
怎么办？
在 宽高设置完100%后加上
min-宽高，这样使得容器的宽高小于这个值的时候不再跟着窗口缩小！
浏览器宽设置 1440px就行

![image-20240701162713513](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240701162713513.png)

```
<div class="box">
  <div class="title">Grail</div>
  <div class="header">header</div>
  <div class="main">
    <div class="aside-left">aside-left</div>
    <div class="content">content</div>
    <div class="aside-right">aside-right</div>
  </div>
  <div class="footer">footer</div>
</div>
```

```
body {
  background: #333;
}

.box {
  display: flex;
  flex-direction: column;
  position: relative;
  width: 608px;
  height: 380px;
  margin: 10px auto;
  border: 1px solid #eee;
  overflow: hidden;
  resize: horizontal;

  .title {
    width: 100%;
    height: 50px;
    color: #eee;
    line-height: 50px;
    text-align: center;
    font-size: 28px;
    font-weight: bold;
    border: 1px solid #eee;
  }
}

.header,
.footer {
  width: 100%;
  height: 60px;
  line-height: 60px;
  text-align: center;
  background-color: #fff;
}

.main {
  display: flex;
  flex: 1;
  width: 100%;
  background-color: #eee;
  
  .aside-left,
  .aside-right {
    flex: 0 0 100px;
    text-align: center;
    line-height: 200px;
    background-color: #ddd;
  }
  
  .content {
    flex: auto;
    text-align: center;
    line-height: 200px;
  }
}
```

弹性项默认只占自己需要的宽度，不声明flex-grow的话


```html
    header nav ul {
        display: flex;
        padding: 0;
        list-style-type: none;
        background-color: #333;
    }
	直接子元素变成弹性项，所以  li  是弹性项，而不是 a
    header nav li{
    }
    header nav li a {
        display: block;
        color: white;
        padding: 14px 16px;
        text-decoration: none;
    }
```

如果不声明flex-grow的话，它们只占用自己的宽度
![image-20240628193855081](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240628193855081.png)?
如果声明的话比如 

```
 header nav li{
 flex-grow:1;
    }
```

![image-20240628193924362](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240628193924362.png)

这样就平均分了







# JavaScript

使用JS最好先写上这个

```
<script src="https://cdn.bootcdn.net/ajax/libs/jquery/3.7.1/jquery.min.js"></script>
```

## 须知

**JavaScript**是一种基于**对象和事件驱动**并具有相对安全性的**客户端**脚本语言，浏览器可以直接编译
举例：数字日历，跑马灯

java是强类型语言，javascript是弱类型语言
强类型：开辟变了存储空间，定了空间将来存储数据的数据类型，只能存储固定类型数据
弱类型：开辟变量存储空间，存啥类型数据都行

具有安全性，简单些，动态性，跨平台性

完整js实现由三部分组成
ECMAScript：核心标准
DOM:文档对象模型
BOM:浏览器对象模型



<font color=229453>举例，将 HTML 代码与 JS 代码耦合</font>
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240622144755990.png" alt="image-20240622144755990" style="zoom:50%;" /> 

### 如何使用？

JavaScript有两种使用方式，一种是直接添加在HTML文档中，另一种是写到外部JavaScript文件，再在HTML中引用该文件
但是 JS代码必须放在标签`<script> </script>`里面



<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240622145336745.png" alt="image-20240622145336745" style="zoom:67%;" /> 

而这个标签`<script>`可以放在任何地方，body里、head里···

但是行业规范：**放在 body 最底部**

> 浏览器加载页面需要时间，加载JS代码也需要时间，用户看到页面加载完成后才会开始操作，所以我们也让网页先加载，后加载JS





与CSS相似，当一段JS代码在多个HTML里使用时，可以单独创建JS文件 而这些JS文件引入的方式是：
`<script src="文件地址"> </script>script>`

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240622145753138.png" alt="image-20240622145753138" style="zoom:80%;" /> 





**内部JS使用举例**

三种消息对话框

1. 警告框
   alert(message)

   ```html
   alert("警告")
   ```

2. 确认框
   confirm(message)

   ```
   confirm("是否确认")
   ```

   <img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240925221615614.png" alt="image-20240925221615614" style="zoom: 50%;" /> 

   点了确认后，这个函数还会有返回布尔值 

   ```
   var inp=confirm("是否确认")
   if(inp==true){
   document.write("确认")
   }else{
   document.write("取消")
   }
   ```

3. 提示框
   prompt(text,defaultText)

   ```
   prompt(”这是提示框","默认文本")
   ```

   <img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240925221838212.png" alt="image-20240925221838212" style="zoom:50%;" /> 

   这个点击确定后也有返回值，返回值就是这个框里的内容，可以接收

   ```
   var ys=prompt("这是提示框")
   if(ys!=''){
   document.write("你好")
   }
   ```

   



### 规范

JavaScript对大小写严格区分，无论是变量，函数名，运算符或者其他，大小写不同那就是不同的内容

JavaScript分号不必要，但是最好加上

JavaScript注释
单行注释： 两个斜杠 //
多行注释: 	/* */

JavaScript代码块 {  }



## JavaScript变量

### 变量声明

JavaScript是弱类型语言，所有数据类型统一用  关键词 var声明

```
var x = 2;
var msg = "Hello JavaScript"
var name;
```

当变量的赋值为文本时，需要用单引号或者双引号括起来

JavaScript可以用一个var同时定义多个变量，也可以赋不同值

```
var x1,x2,x3;
var x1 = 1,x2="hello", x3;
```

由于是弱类型语言，所以同一个变量可以存放不同类型的值

```
var x = 99;
x = "hello"
那么x存的值从数字99变成字符串hello
```

变量的声明不是必须的，可以不用关键词var声明

```
msg1 = "hello";
msg2 = "JavaScript"
msg3 = msg1 + msg2
alert(msg3)//结果是 helloJavaScript
```

当程序遇到未声明过的名称时，会使用该名称自动创建一个变量并继续使用

变量名字的首位字符必须是26个字母或者下划线__或者美元符号$
 其他位置随意

JavaScript变量命名不能和现有关键字和保留字重复
<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240925225316489.png" alt="image-20240925225316489" style="zoom: 67%;" />

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240925225327161.png" alt="image-20240925225327161" style="zoom:67%;" /> 





### 数据类型

| Type         | Exp                                     |
| ------------ | --------------------------------------- |
| 数字number   | let length=16;                          |
| 字符串String | let name="pang"                         |
| 布尔boolean  | let flag=true;                          |
| 空null       |                                         |
| 对象 object  | let x={firstName:"john",lastName:"Doe"} |
| 数组         | let cars=["BMW","VOLOV"]                |
| 函数         | funciton name(参数123){函数体}          |

利用typeof（变量名）方法可以获得变量存储的数据类型

```
var x = "hello";
var y = typeof(x);
var y = typeof x;不加括号也行
```



#### Undefined

所有Undefined类型的输出值都是Undefined
当输出变量从未声明过或者声明了但是未赋值的变量输出都是Undefined

#### Null

表示变量内容为空，可以用于初始化变量或者清空已经赋值的变量

#### String

字符串，用单双引号包括都行
如果字符串本身带有单双引号，用不同的引号包括它
msg="123"  msg='123' msg="1'2'3" msg='1"2"3'

1. 字符串长度
   字符串长度，在字符串中每一个字符都有固定的位置，从0开始
   .length可以获得字符串长度，即字符串中字符个数 

   ```
   var msg = "hello world"
   alert(msg.length)
   ```

2. 获取单个字符
   用方法 **charAt(ind)**可获得指定位置上的字符
   用 **charCodeAt(ind)** 可以获得它的ASCII码值

3. 连接字符串
   方法 **concat(str1,str2,···)**可以连接若干字符串，效果跟+相同
   所以也可以用 + 直接连接

4. 查找字符串
   方法 **indexOf(str,ind),lastIndexOf(str,ind)** 可以查找字符串中是否包含指定字符串内容
   str是要查找的字符串内容，ind是从哪儿开始，last是倒着查
   存在则返回指定内容首个字符的下标，不存在则返回-1

   比如  msg.indexOf(msg1,0) 

5. 查找与替换字符串
   使用 match() || search() 可以查找匹配正则表达式的字符串内容
   match(regExp)------------------match的语法格式
   regExp填入正则表达式 match(/a/g)表示全局查找字母a 小写字母g代表全局查找，返回值为所有符合条件的字符串片段
   search(regExp)------------------search的语法格式
   regExp同样插入一个正则表达式，返回值是匹配条件的字符出串的索引值

   在JavaScript中使用replace()方法可以替换匹配正则表达式的字符串
   replace(regExp,replaceText)-----------Syntax
   regExp填入正则表达式，replaceText填入想要换成的字符串
   replace(/a/g,"A") 把所有小写a换成大写A，返回值是替换完毕的新字符串

6. 获取字符串片段
   **slice() || substring()**截取字符串片段
   slice用于去掉指定片段
   substring用于节选指定片段

   **slice(start,end)** [start,end)这个区间的字符串会被删除
   end忽略则表示从start到尾，如果是负数，则从最后一个位置开始计算，-1表示倒数第一个字符
   返回去除后的字符串

   **substring(start,end)** [start,end) 获取字符串片段
   end为非负数时，两者用法完全相同，但是参数存在负数时，substring会将其视为0
   返回获取到的字符串片段

   ```
   var msg="happy"
   var result1 = msg.substring(1,-1)//返回h
   substring负数会被转换成0  所以是 1,0 从0到1，但是不包括0，结果是h
   从第1个到第0个
   var result2 = msg.slice(1,-1)//返回值为app
   从1到倒数第一个
   ```

7. 大小写转换

   对于字符串类型变量可以使用 toLowerCase() 和 toUpperCase() 转换大小写字母
   前者将全部转换为小写，后者全部转换为大写，返回值是转换完成的字符串

   ```
   var msg = "Happy"
   msg.toLowerCase() //happy
   msg.toUpperCase() //HAPPY
   ```

8. 转义字符
   <img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240926123337948.png" alt="image-20240926123337948" style="zoom:50%;" /> 

#### Number

number类型表示数字，可以是32位以内整数或者64位以内浮点数
也支持科学计数法，八进制和十六进制的表示方式

```
var x = 9;
var y = 3.14;
```

科学计数法

```
var x1 = 3.14e8  3.14*10^8^
var x2 = 3.14e-8 3.14*10^-8^
```

八进制数需要用数字0开头，后面的数字只能0-7（八进制）

```
var x = 010 相当于十进制的8
```

 十六进制数 用数字0和字母x开头，后面字符只能是0-9或A-F，大小写不限

```
var x =0xA 相当于十进制的10
```



浮点数
定义浮点数必须使用小数点，小数点后面至少跟一位数字

```
var x = 3.14
var y = 5.0
如果小数点前面整数位是0，可以省略0
var x = .15  等同于 0.15
```

浮点数可以使用 **toFixed()**方法规定小数点后保留多少位小数
toFixed(digital)

遵循四舍五入的规律，即使后面是0也会保留

```
var x=3.1415926
var result = x.toFixed(2);返回值 3.14
var x = 0.9999
result = x.toFixed(2); 返回值 1.00
```

但是浮点数计算有时会产生误差，建议先扩大成整数，再缩小成小数

```
var x = 0.7 + 0.1
alert(x) ;//0.799999999  而不是 0.8
最好乘十后再除十
```



 特殊Number值

1. infinity
   表示无穷大的含义，有正负之分，数值超过了JS允许的范围后，会显示Infinity或者-Infinity

   ```
   var x = 9e3000
   alert(x) //返回值为 Infinity
   ```

   两个不同数字比较大时，返回值都是Infinity，认为两个数是相等的

   ```
   var x1 = 9e3000
   var x2 = 8e3000
   alert(x1==x2)//返回值为true
   ```

   0作为除数不会报错，正数除以0 为Infinity，负数为-Infinity 0%0为NaN

   Infinity不可以与其他数字进行数学计算，返回值是 NaN

2. NaN
   表示非数字，用于表示数据转换成Number失败的情况，从而无需抛出错误异常
   NaN由于不是数字，也不能用于数学计算，两个NaN也不相等

   ```
   var x = "red"
   var result = Number(x) //返回 NaN
   ```

   JS提供了判断数据类型是否为数值的方法 isNaN() 返回布尔值
   当检测的数据无法转化为Number时返回真，否则返回假 用法  isNaN(变量名)

   ```
   var x1 = "Red"
   var result = isNaN(x1) //true
   var x2 = "666"
   var result = isNaN(x2) //false
   ```

#### Boolean

可以直接用 true || false 表示







#### 模板字符串

模板字符串：**允许嵌入表达式的字符串常量**
模板字符串**使用反引号(\`\`)**代替普通字符串的 双引号/单引号
模板字符串可以包含**特定语法** : `${expression}`占位符
<font color = grey>占位符中的表达式会跟文本一起传给某个默认函数，该函数将他们连接起来</font>

```
let cid=1;
let hid=2;
let res="/courses/"+cid+"/homework/"+hid;
let res2=`/courses/${cid}/homeword/${id}`;
res和res2效果一样, 明显后者更具可读性
```

#### JSON

##### 对象

javascript objects，js里的对象
JSON通过**文本描述**JS对象，方便传递JS对象
<font color = grey>完完全全用字符串描述对象，对象的所有属性都当作字符串传递</font>
JSON的属性以 **键值对形式** 保存

```
{"type":"fiat","model":"500","color":"white"}
```

> 为什么会产生JSON?
> 不同程序语言均通过`对象`封装数据信息，但不同语言编写的程序之间无法直接传输对象互交
> JSON将各种语言的对象，转为文本字符串描述；
> 将描述对象的字符串，通过标准的通用的HTTP协议传输，从而极简洁的实现了异构系统之间的互交

```
{
"user":{"name":"pang","role":"3"}
"courses":[{"id":1,"name":"java"},{"id":2,"name":"C++"}]
}
```

一个JSON，包含若干属性👆
user属性，是一个包含若干属性的对象
courses属性，是一个数组，包含若干对象，对象又各自包含属性

#####  方法

对象中的方法

```
let person={
firstName:"John",
lastName:"Doe",
id:556,
getFullName(){
return `${this.firstName}/${this.lastName}`;
}
};
一个person对象，具有若干属性（属性以键值对的形式保存）
里面还有一个方法，对象中的方法 而非函数
不应该使用箭头函数，否则this会指向错误
```

那么对象中的属性方法怎么调用呢？
跟java一样  `对象.属性/方法`调用
与java不同 JS不对外暴露getter/setter 而是直接调用

```html
<body>
<button type="button" onclick="show()">点击取值</button>
<div id="demo">被替换喽</div>
<script>
    let person={
        firstName:"John",
        lastName:"Doe",
        id:556,
        getFullName(){
            return `${this.firstName}/${this.lastName}`;
        }
    };
    let show=()=>{
        document.getElementById("demo").innerHTML=person.getFullName();
    }
</script>
</body>
```



### 类型转换

1. 转换成字符串
   布尔型和数字类型可以用 toString() 方法把值转换为字符串类型

   布尔型的 toString方法只返回 true或者false,因为布尔值只有 true或者false

   ```
   var x = true
   x.toString() //true
   ```

   数字类型使用 toString() 方法有两种模式，分为默认模式和基数模式
   默认模式中,toString()不带参数直接使用，此时，用任何形式表示的数字都会转换为十进制数字显示

   ```
   var x1=99.90;
   var x2=1.25e3;
   x1.toString(); //99.9
   x2.toString(); //1250
   ```

   基数模式，需要在toString()的内部填入一个指定的参数，根据参数把原始数据转化为二进制，八进制，或者十六进制
   什么？你问十进制在哪？他不是在默认模式里吗

   ```
   var x = 10
   x.toString(2) 转为2进制
   x.toString(8) 转为2进制
   x.toString(16) 转为2进制
   ```

2. 转换成数字
   JS提供了两种将String类型转换为Number类型的方法
   parseInt() 和 parseFloat()
   前者转换为整数，后者转换为浮点数，仅适用于对String的转换，其他类型返回值是NaN

   parseInt() 从左到右检查每个位置上的字符，如果是有效数字则转化为Number类型，发现不是数字就停，返回至此已经转换的值
   如果第一个就不是有效数字，直接返回NaN.  由于这个是转换整数 所以小数点不算有效数字，从而终止检测和转换

   ```
   var x = 123hhh34
   parseInt(x) //124
   var y = hh123hh23
   parseInt(y) //NaN
   ```

   该方法还可以设置第二个参数，同样是 2，8，10，16转换成各自进制的数字

   特殊情况：如果字符串原始数据为十进制数，但是开头是0，那么需要用第二个参数强调一下转换进制，否则会被转为八进制

   ```
   var x = "010"
   parseInt(x) //8
   parseInt(x,10) //10
   parseInt(x,8) //8
   ```

   parseFloat()与前者相似，不过**首次出现**的小数点认为是有效字符，但是后面的小数点依然是无效字符

   ```
   var x = "hello3.14"  parseFloat(x) //NaN
   var y = "3.14hello"  parseFloat(y) //3.14
   var z = "3.14.15"	 parseFloat(x) //3.14	
   ```

   还有不同之处，就是只接收十进制数，如果八进制数前面带有0，会直接忽略这个0，按十进制数看

   ```
   var x = "010"
   parseInt(x) //10
   ```

   而接收了十六进制数，十六进制由 0x开头，因此先忽略这个0后检测的第一个字符为无效字符 返回NaN

### 强制类型转换

一些值无法通过 toString parseInt parseFloat 转换，例如null undefined等
此时可以用JS中的强制转换对其转换

1. Boolean() 
   所有类型都可以用该函数转换成布尔值 
   Boolean(x) 
   x是字符串的情况下  x非空时返回true，否则返回false
   x是数字的情况下，x=0返回false，x为其余整数或者浮点数都返回true
   x为null或者undefined时，返回false
   如果x本身就是布尔值，则返回x

2. Number（）函数
   将任意类型转换成数字
   如果转换内容为合法的整数或者小数时，会自动调用 parseInt 或者 parseFloat
   但是与调用他们也有点不同，如果数字后面超过一个小数点或者有其他无效字符，返回NaN而不是截至数字
   如果转换布尔值 true转成1，false转成0
   null->0 undefined->NaN
   如果是其他自定义对象调用这个方法，返回NaN

3. String(value)函数
   强制转换为字符串类型并且保留字面内容，与toString()相似，与其不同的是它可以将NULL和undefined类型也转成字符串

   ```
   var x = null;
   var result = String(x) //"null"
   var result = x.toString() //发生错误 无返回值
   ```

   

### 操作符

| 算数运算符 | Description |
| ---------- | ----------- |
| +          | 加          |
| -          | 减          |
| *          | 乘          |
| /          | 除          |
| %          | 求余        |
| ++         | 自增        |
| --         | 自减        |



| Assignment Operator | Description                                |
| ------------------- | ------------------------------------------ |
| =                   | 赋值运算符<br />可用于赋值<br />可用于改值 |
| +=                  | x+=y \| x=x+y                              |
| -=                  | x-=y \| x= x-y                             |
| *=                  | x*=y \| x=x*y                              |
| /=                  | x/=y \| x= x/y                             |
| %=                  | x%=y \| x=x%y                              |



| 逻辑运算符 | Description        |
| ---------- | ------------------ |
| ==         | 等于               |
| ===        | 类型和值全部相等   |
| ！=        | 不等于             |
| ！==       | 类型和值有一个不等 |
| > < >= <=  | 大于小于等于       |
| ?          | a>b?a:b            |

双等号== 判断两个数值是否相等
如果两个值均为数字类型，则直接判断
如果存在其他数据类型，则尝试转换成数字类型再比较，转换规则如下







全等于运算符由三个等号===组成，也用于判断两个值是否相同
但是判断前不进行任何的类型转换，也就是说，两个值必须数据类型相同，数值也相同才返回true

```
var x = 99
var y = '99'
x==y //true
x===y //false
```



| Type operator | Descripiton                              |
| ------------- | ---------------------------------------- |
| typeof        | 返回变量的类型                           |
| instanceof    | 如果对象是某个对象类型的实例的话返回true |

计算方向

js从左到右按类型合并推导
let x=16+"A" -> 16A
let x=16+4+"A" ->20A
let x="A"+16+4->A164
如果Number在前面，按number加。直到遇到String
如果String在前面，后面的全部按照String来直接拼接





### 循环语句

有四种类型的循环语句

- for
- for-in 循环遍历对象的属性
- while
- do-while

for

```
循环变量在里面声明
for(var i=0;i<10;i++){

}
循环变量在外面声明
var x=0
for(;x<10;i++){

}
```

for-in
用于遍历对象的的所有属性和方法
每次循环，x都取people的某个属性或者方法名

```
for(x in object){
代码块
}

var people = new Object();
var msg="";
people.name="marry";
people.age="20";
people.major="JAVA";
for(x in people){
msg+=people[x]  对象[属性]用于取值
}
alert(msg)//marry20JAVA
```

while
条件为真再做

```
while(条件表达式){
代码块
}
```

do-while
不管怎么样，先做一次再说

```
do{
代码块
}while(条件表达式)
```





break continue
break终止一层循环
continue 终止一次循环



## 对象类型

JS对象分为 本地对象 内置对象 宿主对象 三种
本地对象 时ECMAScript定义的引用类型
内置对象时无需实例化直接可以使用的对象，也是特殊的本地对象
宿主对象指的是用户的机器环境，包括DOM,BOM

### 本地对象

分为四种 数组Array  日期Date 正则表达式RegExp  对象 Object

#### 数组Array

用于在单个变量里存储一系列的值

```
var mobile = new Array();
var mobile[0]="apple";
var mobile[1]="huawei";
var mobile[2]="xiaomi";
```

数组是从0开始算的，Array类型的特点是无需在一开始就声明数组的具体元素数量，可以随用随加
如果一开始就知道有什么元素，可以用逗号隔开直接创建

```
var mobile= new Array("apple","huawei","xiaomi")
或者
var mobile=["apple","huawei","xiaomi"]
```

Array对象包括了length属性，代表数组里元素个数 没有则返回0

```
var mobile= new Array("apple","huawei","xiaomi")
mobile.length //3
```

#### 日期Date

有四种初始化方式
new Date() 获取当前的日期和时间

```
alert(new Date())
```

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240926170304208.png" alt="image-20240926170304208" style="zoom:50%;" /> 

new Date(dateString) 使用表示日期时间的字符串定义时间

```
alert(new Date("May 10,2000,12:12"))
```

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240926170546904.png" alt="image-20240926170546904" style="zoom:50%;" /> 

new Date(milliseconds)  使用1970年1月1日8时到指定日期的毫秒数定义事件，如输入12

```
alert(new Date(1000))  从1970年1月1日 过了1000毫秒，也就是  1秒
```

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240926170703969.png" alt="image-20240926170703969" style="zoom:50%;" /> 

new Date(year,month,day,hours,minutes,seconds,milliseconds)
自定义年月日时分秒毫秒，缺项默认为0

```
alert(new Date(2024,9,26,17,8,2000))
```

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240926170900540.png" alt="image-20240926170900540" style="zoom:67%;" /> 



日期对象也有很多方法
<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240926171049627.png" alt="image-20240926171049627" style="zoom:67%;" /> 

```
var date = new Date();
var year = date.getFullYear();
var month = date.getMonth();
var day = date.getDate();
var week = date.getDay()
alert("year="+year+"month="+month+"day="+day+"week="+week)
```

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20240926171326558.png" alt="image-20240926171326558" style="zoom:80%;" /> 

#### 正则表达式

RegExp对象表示正则表达式，通常用于检索文本中是否包含指定的字符串
new RegExp(pattern[,attribute])
pattern为字符串的形式，规定表达式的匹配规则
attributes为可选项，可包含属性g,i,m分别表示全局匹配，区分大小写匹配和多行匹配

```
var pattern = new RegExp([0-9],g);
声明了一个全局检索文本中是否包含0-9之间任意字符的正则表达式
```

还有一种简写 :  /pattern/[attribute]

```
var pattern = /[0-9]/g;
```



#### 对象Object

js对象用于储存键值对，多个键值对之间用逗号隔开

在JavaScript中，对象的键（也称为属性名）通常是字符串类型。
当你创建一个对象并为其属性赋值时，属性名会被自动转换为字符串类型，即使最初你使用的是其他类型的值

```
var obj = {
    name: "Kimi",
    age: 30
};
```









获取对象中的指定属性有两种方法，一种是变量名称后面加 点.属性名 对象.属性
另一种使用中括号和引号 对象["属性名"]

```
var result = student.name;
var result = student["name"];
```

同样的方法可以改变属性值

```
student.name="李四"可以直接改值为李四
```





Json对象

**JSON对象本质上是一个字符串**（字符串，划重点），它表示一个JavaScript对象的结构。
通常，我们使用`JSON.stringify()`方法将JavaScript对象转换为JSON字符串，
		    或者使用`JSON.parse()`方法将JSON字符串转换为JavaScript对象。

Json对象的键必须由 双引号 包裹，也就是键必须是字符串
Json对象的值可以是 任意类型

```
{
  "name": "Kimi",
  "age": 30,
  "isAI": true,
  "skills": ["chatting", "searching"],
  "details": {
    "company": "Moonshot AI",
    "location": "Earth"
  }
}
```





JavaJson对象区别

1. **键的表示**：
   在JSON中，所有的键都必须用双引号（"）包围，键必须是字符串
   在JavaScript对象中，键可以是未加引号的标识符（即不包含空格、特殊字符等的字符串），也可以是字符串（用单引号(')或双引号(")包围）。
2. **值的表示**：
   在JSON中，值是字符串时必须用双引号包围
   在JavaScript对象中，字符串值可以用单引号或双引号包围
3. **函数和方法**：JSON不支持函数和方法，而JavaScript对象可以包含函数作为其属性
4. **特殊值**：JSON支持null这个特殊值，而JavaScript对象中没有这个概念
5. **数据类型**：
   JSON只支持字符串、数字、对象、数组、布尔值和null这几种数据类型
   JavaScript对象可以包含更多类型的值，比如日期对象、正则表达式对象等



### 内置对象

#### Gobal对象

JavaScript中Gobal对象又称为全局对象，其中包含的属性和函数可以用于本地的所有JS对象

属性方法如下表（待补充）





#### Math对象

Math对象用于计算，无需初始化创建。可以直接使用关键词Math调用其属性和方法
常用属性和方法如下（待补充）



### 宿主对象

宿主对象包括HTML DOM 和 BOM





### 遍历

Loop

1. **For Loop**

   ```
   let text="";
   for(let i = 0;i<5;i++){
   text+=`The number is ${i}<br>`;
   }
   document.getElementById("array").innerHTML=text;
   ```

   效果：把id=array的元素替换为text
   ![image-20240622162028946](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240622162028946.png)

   ![image-20240622162042052](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240622162042052.png)

2. **foreach Loop**
   for(let/const var **of** 数组){}
   最好用 const 在循环中防止被修改引用

   ```
   let courses=[
   {id:1,name:"java"},
   {id:2,name:"C++"}
   ];
   for(const c of courses){
   console.log(`${c.id}/${c.name}`);
   }
   ```

   效果：在控制台打印两个 course对象的数据

   控制台在哪？浏览器摁F12
   ![image-20240622162522061](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240622162522061.png)









## JS函数和事件

### 函数

#### 基本语法

```
function 函数名(参数列表){
函数体
}

function welcome(){
alert("welcome to js");
}
```

函数可以在JS代码的任意位置被调用，也可以在指定事件发生时调用

```
<button onclick="welcome()">点击调用</button>
事件绑定，意为发生这个时间时调用这个函数
```

相比Java，JS的函数无需声明返回值类型，如果函数存在返回值，直接return 返回值即可

**常用的系统函数-全局函数**
eval(String) 
里面放一个字符串，js会把这个字符串认作JS代码并且尝试执行，把执行的结果返回去，如果没结果，则undefined

```
 eval("x=20;y=30;z=x*y");
 console.log(z);
 
 运行后控制台打印出600
```







#### **匿名函数**

在函数表达式中省略函数名，也可以用一个变量接收这个匿名函数，然后调用时使用变量名()即可（像是给函数起了个名字）

```js
var fn = function  -此处省略函数名- (num1,num2){
return num1+num2;
}
调用：
fn(1,2)
```

匿名函数自调用
将匿名函数写在小括号内然后对其调用，如果希望某个功能只实现一次可以使用这种方法

```
(function (num1,num2){
console.log(num1+num2)
})(2,3);这个调用的括号紧跟这个函数
```





#### 箭头函数

类似于lambda表达式 (参数)=>{函数}
只有一个参数时，()可以省略；没有参数时()不可以省略
{}里只有一条语句且语句结果就是返回值时，{ }和return 可以省略
=> 用的是=> 不像java是 ->



以小括号开头，里面可以放置参数，后面跟着箭头，箭头后面跟着函数体
(参数)=>{函数体}



箭头函数可以直接赋值给变量，然后可以通过变量名调用这个函数

```html
<script>
let toCelsius=
(f)=>{return(5/9)*(f-32)}
那么这样已经定义了一个函数了
此时 toCelsius 便是函数名 像是给匿名函数起了个名字
它的参数就是匿名函数的参数列表 使用时就是 toCelsius()
document.getElementById("demo").innerHTML = toCelsius(77);
</script>
```

### 事件

事件编程：让用户不仅能浏览页面中的内容，而且还可以和页面元素进行交互
事件类型：鼠标事件，键盘事件，HTML事件，突变事件；
鼠标事件：鼠标单击
键盘事件：按下或者释放按键
突变事件：文档底层元素发生改变时出发的事件

#### 事件句柄

基本语法
\<tag 事件句柄 = "javascript代码" ...> \</tag>

事件句柄
事件句柄是事件发生要做的操作，也称为事件属性
\<body onload = "show() " > ... \</body>
其中 onload便是事件句柄，show() 可以叫做事件处理函数 load叫事件名称

事件句柄一览表

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241002223613896.png" alt="image-20241002223613896" style="zoom: 80%;" /> 









#### 事件处理



当一个事件发生时，如果需要截获并处理事件，只需要定义事件得到事件句柄所关联的处理代码，有三种方式
1.静态指定 
<tag 事件句柄1="处理程序" [事件句柄2="处理程序"] >
一个元素可以绑定多个事件

```
<input type="button" value="通过函数输出信息" onclick="testInfo('单击按钮，调用函数输出信息')">
```

2.动态指定
<事件主角-对象>.<事件句柄>=<事件处理程序>

```
<body>
    <form name="myform" method="post" action="" >
       <input id="input" type="button" name="mybutton" value="提交" > 
    </form>
     <script>
      function clickHandler() {alert("即将提交表单！"); return true;}
      //动态分配一个事件句柄
      document.getElementById('input').onclick=function(){return clickHandler();}
      //myform.mybutton.onclick(); 对象.句柄=程序
      </script>
     </body>
```

3.特定对象特定事件指定
\<script for="对象" event = "事件">处理代码\</script>

```
<body>
    <h4>给特定对象指定特定事件处理程序</h4>
    <script for="window" event="onload">指定window对象触发事件 onload 时 执行其中代码块
        alert("网页读取完成，欢迎光临！");
    </script>
    <body>

```



#### 处理程序

事件处理程序的返回值
在JavaScript中通常事件处理程序不需要有返回值，这时浏览器会按默认方式进行处理
但是很多情况下需要使用返回值，来判断事件处理程序是否正确进行处理
返回值类型：boolean类型。浏览器根据返回值的类型决定下一步如何操作
当返回值为true，进行默认操作； 当返回值为 false，阻止浏览器的下一步操作

基本语法：事件句柄=" return 函数名（参数) ;"

举例↓

```
<script language="javascript">
        function showName() {
            if (document.form1.name1.value == "") {
                alert("没有输入内容！");
                return false;
            } else {
                alert("欢迎你!" + document.form1.name1.value);
                return true;
            }
        }
    </script>
    
<body>
    <h4>事件处理程序返回值的应用</h4>
    <!-- onsubmit事件处理函数返回真值就执行action指定的网页 -->
    <form name="form1" action="simple.html" onsubmit="return showName();">
        姓名：<input type="text" name="name1" />
        <input type="submit" value="提交" />
    </form>
</body>

正常来收，点击表单提交后，正常来说会跳转到action里的URL页面，但是这里给form绑定了事件，当事件处理程序返回false时，便不会跳转
```



#### 表单事件

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241002225115665.png" alt="image-20241002225115665" style="zoom: 67%;" /> 



获得/失去焦点事件

什么是焦点？鼠标点击便是焦点
如果鼠标点击了A，那么A获得焦点。
只要鼠标没有再次点击别的地方，那么焦点一直属于A。

```
<form action="http://bilibili.com">
    <input type="button" value="获得/失去焦点" onfocus="getFocus()" onblur="loseFocus()">
</form>

function getFocus(){
    document.body.style.backgroundColor="green";
}
function loseFocus(){
    document.body.style.backgroundColor="red";
}
```



提交及重置事件

```
    <script  type="text/javascript">
        function submitTest() {
            var msg ="表单数据的获取：\n";
            var username = document.getElementById("input1").value;
            msg+="用户名:";
            msg+=username;
            var psw = document.getElementById("input2").value;
            msg+="，\n密码:是";
            msg+=psw;
            alert(msg);
            return false;//获取但是不提交表单
        }
        function resetTest() {alert("将数据清空");}
    </script>
    
    <body>
        <form onsubmit="return submitTest();"  onreset="resetTest()"> 
            <fieldset>
                <legend>表单数据提交</legend>
                <br><label>用户名：</label><input type="text" id="input1">
                <br><label>密&nbsp;码：</label><input type="password" id="input2">
                <br><input type="submit" value="提交">
                <input type="reset" value="重置">
            </fieldset>
        </form>
    </body>
```



改变以及选择事件

```
    <script language="javascript">
        function changeImage() {            
            var a = document.getElementById("game").selectedIndex;
            //获取下拉框中选择项
            document.getElementById("show").src = document.getElementById("game").options[a].value;
			//将图片更改为对应选择项
        }
    </script>
        <form>
        <select id="game" onChange="changeImage()" >
            <option value="pic4.jpg">--请选择--</option>
            <option value="pic0.jpg">平板电视</option>
            <option value="pic1.jpg">笔记本电脑</option>
            <option value="pic2.jpg">单反相机</option>
            <option value="pic3.jpg">智能手机</option>
        </select>
    </form>
```



#### 鼠标事件

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241003145930647.png" alt="image-20241003145930647" style="zoom:67%;" /> 



鼠标单击事件

```
    <script type="text/javascript">
        function $(id) { return document.getElementById(id); }
        function copyText() { $("target").value = $("source").value; }
        //$("target")突然出现的？上面定义的函数在这儿被调用了
    </script>
    <form method="post" action="">
        来源文本框：<input type="text" id="source" value="">
        <br>目标文本框：<input type="text" id="target" readonly>
        <br><input type="button" value="复制文本框内容" onclick="copyText();">
    </form>
通过ID获取页面元素的通用函数 
function $(id){ return document.getElementById(id); }
```

鼠标移动事件

```
function mouseOver(){
    document.getElementById("i1").src="resource/img/stq.png";
}
function mouseOut(){
    document.getElementById("i1").src="resource/img/Varolant.jpg";
}
<body>
    <img id="i1"src="#" alt="" onmouseover="mouseOver()" onmouseout="mouseOut()">
</body>
网页里有个图片，鼠标移动上去是一个图，移出去是另一个图
```

#### 键盘事件

<img src="https://cdn.jsdelivr.net/gh/Hushyo/img@main/img/image-20241003151024290.png" alt="image-20241003151024290" style="zoom:67%;" />  

通过 window的event对象的keyCode属性来获取按键代码的值
回车：13，
0～9：48～57;
Aa～Zz: 65～90;  
对应代码值是ASCII码值
event对象的key属性则是直接返回按下按键的字符
按 A 时 key->"A"  keyCode->65

等待学习





## DOM





### 概述

DOM是W3C设计的，与具体开发语言无关的一套接口，接口中定义了操作文档的，内容/结构/样式等等的方法
当网页被加载时，浏览器会创建页面的文档对象模型
HTML DOM 模型被结构化为 对象树：
<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240622160156050.png" alt="image-20240622160156050" style="zoom:50%;" /> 

通过这个对象模型，JavaScript获得动态创建HTML的所有力量！

- JavaScript能改变页面中的所有HTML元素，属性，样式
- JavaScript能删除和添加HTML元素和属性
- JavaScript能对页面中所有已有的HTML事件做出反应，而且可以创建新的HTML事件

#### 节点

节点Node，是构成我们网页的最基本的组成部分，网页中的每一个部分都可以称为是一个节点
比如 html标签、属性、文本、注释、整个文档等 都是一个节点
虽然它们都是节点，但是它们的具体类型是不同的
常用的节点类型：

- 文档节点: 整个HTML文档
- 元素节点: HTML文档中的HTML标签
- 属性节点: 元素的属性
- 文本节点: HTML标签中的文本内容

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240622160620488.png" alt="image-20240622160620488" style="zoom:50%;" /> 

#### 文档节点

文档节点（Document）代表的是整个HTML文 档，网页中的所有节点都是它的子节点。
document对象作为window对象的属性存在的，我们不用获取可以直接使用。
通过该对象我们可以在整个文档访问内查找节点对象，并可以通过该对象创建各种节点对象。

#### 元素节点

HTML中的各种标签都是元素节点（Element），这也是我们最常用的一个节点。
浏览器会将页面中所有的标签都转换为一个元素节点， 我们可以通过document的方法来获取元素节点。
例如：`document.getElementById()`，根据id属性值获取一个元素节点对象。

#### 属性节点

属性节点（Attribute）表示的是标签中的一个一个的属 性，这里要注意的是属性节点并非是元素节点的子节点，而是元素节点的一部分。可以通过元素节点来获取指定的属性节点。
例如：`元素节点.getAttributeNode("属性名")`，根据元素节点的属性名获取一个属性节点对象

> 我们一般不用属性节点

#### 文本节点

文本节点（Text）表示的是HTML标签以外的文本内容，任意非HTML的文本都是文本节点，它包括可以字面解释的纯文本内容。文本节点一般是作为元素节点的子节点存在的。获取文本节点时，一般先要获取元素节点，在通过元素节点获取文本节点。
例如：`元素节点.firstChild;`获取元素节点的第一个子节点，一般为文本节点。

### 查找HTML元素

有三种方法查找HTML元素

- 通过ID名查找
- 通过标签名查找
- 通过类名查找

| 方法                                      | 介绍                      |
| ----------------------------------------- | ------------------------- |
| document.getElementById( *id* )           | 通过元素 id 来查找元素    |
| document.getElementsByTagName( *name* )   | 通过标签名来查找元素      |
| document.getElementsByClassName( *name* ) | 通过类名来查找元素        |
| document.querySelector(*CSS选择器*)       | 通过CSS选择器选择一个元素 |
| document.querySelectorAll(*CSS选择器*)    | 通过CSS选择器选择多个元素 |

如果查找不到则返回null，查找到会以对象的形式返回
通过ID查找到单个元素

```
var test = document.getElementById("test");
var result = test.innerHTML;
查找 id = "test" 的元素并获取内部文本内容
```

标签名和类名不像ID一样是唯一的，如果查找不到则返回null，如果查找到会返回数组

通过标签名查找到一个或者一系列元素

```
var p = document.getElementsByTagName("p");

var result = p[0].innerHTML;
查找所有段落元素并获取第一个段落的文本内容
```

通过类名查找一个或者多个元素

```
跟 tagname差不多
```







### 取改HTML值

创建动态的HTML内容，使用 document.write()方法可以往HTML页面动态输出内容

```
document.write("hello world") 页面上会输出字符串hello world
注意 \n在这里是无效的，HTML想换行要输入 <br>
```



**改变HTML元素内容**

innerHTML方法，既可以用于获取元素内容，也可以用于改变元素内容
`var 变量名 = 元素对象.innerHTML`；  获取元素内容
`元素对象.innerHTML = 新的内容`;   改变元素内容



**改变HTML元素属性**
根据元素的属性名 可以获得也可以更改元素内容

`元素对象.属性名 = 新的属性值`

```
var img = document.getElementById("image");
img.src="新URL";
```

也可以用 setAttribute()方法修改属性

`元素对象.setAttribute(" 属性名 "，"新的属性值")`;

```
var img = document.getElementById("image");
img.setAttribute("src","新URL")
```



**改变HTML元素样式**
注意样式跟属性不是一回事，样式算是属性style的子项
所以不能使用setAttribute("样式名"，“样式属性”)这样来更改样式，改样式有别的方法
`元素对象.style.样式属性 = 新的值`;

```
var test = document.getElementById("test");
test.style.backgroundColor="blue";元素背景改成蓝色

或则
document.getElementById("test").style.backgroundColor="blue";
```



### **DOM事件**

js可以在HTML页面状态发生变化时执行代码,这种状态变化被称为DOM事件

dom事件也是属性的一种
js代码可以直接作为属性值写进去，也可以写成js函数然后调用

| Event       | Description        |
| ----------- | ------------------ |
| onchange    | HTML元素被修改时   |
| onclick     | 用户点击HTML元素时 |
| onmouseover | 鼠标在HTML元素上时 |
| onmouseout  | 鼠标从元素上移开时 |
| onkeydown   | 按键按下时         |
| onload      | 浏览器加载完成时   |

```
<button onclick="alert("hi")">点击弹出hi</button>
这个是个错误示范↑正确写法如下
<button onclick="alert('hi')">点击弹出hi</button>
由于属性值需要用双引号包括，所以内部需要双引号时，要用单引号代替
```



使用JS也可以为HTML页面动态添加和删除HTML元素
添加HTML元素
分为两个步骤，先**创建HTML元素**，然后将其追加在一个已经存在的元素中去
document对象的createElement()方法可以创建新的元素
创建出来不意味着添加到页面里

```
document.createElement("元素标签名");
document.createElement("p");
```

再**追加HTML元素**，追加进去才算添加到页面里

```
已存在的元素对象.appendChild(将要添加的元素对象);
var p =document.createElement("p");
var test = document.getElemEntById("test");
test.appendChild(p);
```

删除HTML元素

也需要两个步骤，先获取想要删除的元素对象，然后用removeChild方法将其从父元素中移除

```
如果父元素有ID或者其他方式能获得到，直接获得即可
var test = document.getElementById("test")//父元素
var p = document.getElementById("p1");想要删除的元素
test.removeChild(p);

如果父元素无法通过ID获取，可以通过子元素的parentNode属性获取
var p = document.getElementById("p1");
var test = p.parentNode;
test.removeChild(p)
```





DOM事件流
事件流分为事件捕获和事件冒泡
事件捕获由网景公司的团队提出，指的是事件流传播的顺序应该是从DOM树的根节点一直到发生事件的节点；
事件冒泡由微软公司的团队提出，指的是事件流传播的顺序应该是从发生事件的节点到DOM树的根节点；

W3C对网景公司和微软公司提出的方案进行了中和处理，将DOM事件流分为3个阶段
事件捕获阶段：事件从document节点自上而下向目标节点传播的阶段。
事件目标阶段：事件流到达目标节点后，运行相应的事件驱动程序的阶段。
事件冒泡阶段：事件从目标节点自下而上向document节点传播的阶段。

当事件发生后，浏览器首先进行事件捕获，但不会对事件进行处理，然后进入事件目标阶段，运行目标节点的事件驱动程序，最后进入事件冒泡阶段，逐级对事件进行处理。

下面以一个包含div元素的页面为例，展示事件流的具体过程

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20241002211910582.png" alt="image-20241002211910582" style="zoom:50%;" />  

## BOM

浏览器对象模型，使得JS可以与浏览器交互
BOM常用对象如下
window：浏览器窗口对象，成员包括所有全局变量，函数和对象
screen：屏幕对象，常用于获取用户可用屏幕的宽和高
location：位置对象，获取当前页面的URL地址，还可以重定向
history：历史记录对象，包含了浏览器的浏览历史记录
navigator：浏览器对象，通常用于用户浏览器的相关信息

### window

JS中window对象表示浏览器窗口，JS中一切全局变量，函数和对象都自动称为window对象的内容
比如 alert() 完整写法为 window.alert() 通常情况下 window.可以省略不写

###  Screen

js中window.screen对象可以获取屏幕的宽和高，使用时可以省略前缀，直接写作screen
screen常用属性如下
availWidth:表示屏幕可用宽度 单位为px
availHeight:表示屏幕可用高度，单位px

### Location

window.location对象可以获取当前页面的URL或者重新定向浏览器，也可以忽略window前缀直接写作location

location的href属性可以用于重新定向

```
location.href="http://bilibili.com";
```



### History

window.history是历史记录对象，包含浏览器的历史记录
实现浏览器上返回和前进按钮的相同功能，同样可以省略window前缀直接写为history

| 方法            | 说明                                                         |
| --------------- | ------------------------------------------------------------ |
| forward()       | 加载history列表中下一个URL                                   |
| back()          | 加载history列表中上一个URL                                   |
| go(number\|URL) | 加载列表中某个页面 URL指定要访问的URL<br />number指定URL在history URL列表中的位置 |

### Navigator

window.navigator对象可获取用户浏览器一系列信息，如浏览器名称版本号等等

可简写为 navigator





















# jQuery

轻量，隐式迭代，链式编程，操作行为与HTML文档分离·····

jQuery 是一个高效、精简并且功能丰富的 JavaScript 工具库。
它提供的 API 易于使用且兼容众多浏览器，这让诸如 HTML 文档遍历和操作、事件处理、动画和 Ajax 操作更加简单。
目前超过90%的网站都使用了jQuery库
jQuery的宗旨：写的更少，做得更多！

将jQuery代码置于文档完全加载后执行



> VUE3不推荐使用jQuery



## jQuery引入

- jQuery必须引入项目里面才能使用 jQuery 的内容
  之前的JS必须引入东西才能用应该是记错了，js代码可以直接用，只有jQuery才需要引入

- 引入有两种方式，一种是下载jQuery文件到项目里，也就是本地引入
  另一种是 引用网络节点提供的jQuery文件而无需在项目中包含jquery文件，减少项目体积

- 不管是哪种，都需要通过 \<script src="url">  \</script>把它引入

1. 本地引入：将jQuery下载下来然后导入项目中，通过script标签引用

   ```
   <head>
       <script src="jquery-1.9.1.min.js"></script>
   </head>
   ```

2. CDN引入：使用远程CDN资源库在线引入，避免了文件下载

   ```
   <head>
       <script src="https://cdn.bootcdn.net/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
   </head> 
   ```



## jQuery Syntax

- **基础语法结构**
  **$( selector ).action( )**
  $表示 jQuery 语句，选择符 selector用于选择HTML元素
  action( )到时候会换成具体的函数，表示执行什么动作

- 在引入jQuery文件后，全局作用域里会出现两个变量  $ 和 jQuery 
  这两个变量引用的是同一个对象----**jQuery 顶级对象**

- 方便书写，我们经常用 $ ，其实 jQuery(selector).action()也可以的

例子: $('div').hide() 隐藏页面里所有div元素



**jQuery顶级对象相当于一个构造函数**，用于**创建jQuery实例对象而不用使用 new 关键字**
它的内部会自动进行实例化，然后返回实例化的对象，jQuery对象本质是 jQuery顶级对象对DOM对象包装后产生的对象

jQuery对象其实是一个集合
`$("selector")` 会根据提供的选择器 `selector` 来选取匹配的 DOM 元素集合
根据提供的选择器选择所有匹配的DOM元素哦！这些元素变成一个jQuery对象！



jQuery对象 跟 DOM 对象 不是一回事

实际开发中会经常遇到 jQuery对象和DOM对象之间进行转换
DOM对象比jQuery对象更加复杂，DOM对象的一些属性和方法在jQuery对象中没有封装
用到这些方法或者属性时需要把jQuery对象转换成DOM对象

- jQuery对象转DOM对象，两种实现方式
  jQuery对象[索引]  或者 jQuery对象.get(索引)

  ```
  var div1 = $('div')[0];
  var div2 = $('div').get(0);
  ```

- DOM对象转jQuery对象
  $(DOM对象)

  ```
  var div = document.getElementById('id');
  var jQueryDiv = $(div);
  ```

  

如果选择器中的属性值本身不包含空格或其他特殊字符，是可以不用引号的。
这包括了大部分的情况，比如 `name`、`id`、`class` 等常见的属性选择器。

```
let radios = $("input[name=future]");
let radios = $("input[name='future']");
```



**文档就绪函数**

为了避免文档在加载完成前就运行了jQuery代码导致潜在的错误，所有的jQuery函数都要写在一个文档就绪函数中
错误举例：HTML页面未加载完成，但是jQuery却想要调取某个未加载完的HTML元素

文档就绪函数写法如下

```
$(document).ready(funciton(){
jQuery函数内容
})
```

document本身就是一个DOM对象，准备就绪后执行函数 函数内写的是jQuery函数内容，其实也能写正常的js代码

```
$(document).ready(funciton(){
alert('加载完成')
})
```



### **基本选择器**

**标签选择器**

\$("标签")
\$("div") 选中页面中所有的 div 标签
![image-20240702174511493](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240702174511493.png)

通过 元素选择器 div 选中了页面里所有的 匹配的DOM元素，然后统一设置css样式

**id选择器**

\${"#id"}
\${"#btn"} 选中页面中所有id为btn的元素(但事实上id只有一个元素能用，他选中的是第一个)

**class选择器**
\${".class"}
\${".red"} 选中页面中所有 class="red" 的元素

**通配符选择器**

\${"Selector1 Selector2"}
\${".content *"} 选中页面中 class="content" 的元素下的所有元素

**并集选择器**	

\${"Selector1,Selector2,Selector3"}  选择器间用逗号隔开，如果是空格，那就变成通配符了
${"div,p"}=>所有div元素和p元素

**交集选择器**	
\${"Selector1Selector2"}
\${"div.class"}  选中页面所有 class="class" 的div元素

**层级选择器**
\${"Selector1>Selector2"}
${"ul>span"} 选中页面中所有ul下的直接span元素

**后代选择器**
\${"Selector1 Selector2"}
\${"ul span"} 页面中ul下的 span元素

**兄弟选择器**
\${"Selector1+Selector2"}
\${"#box+li"}选中 id="box" 的下一个兄弟li

\${"Selector1~Selector2"}
\${"#box~li"} id="box" 下面的同级 li元素

### **过滤选择器**

**基本筛选器**
:even代表选取下标为偶数的行
\${"tr:even"} 
:odd 代表选取下标为奇数的行
\${"tr:odd"}
:first 选取第一个
${"p:first"} 选中页面里的第一个 p  元素
:last 选取最后一个
\${"p:last"} 选中页面中最后一个 p 元素

**属性选择器**

由于里面的属性如果要指定值的话，也要用到引号，但是双引号已经在外围了，里面不能用双引号，所以里面用单引号

\$("[属性]")
\$("[href]") 选中显式声明了 href  属性的元素

```html
<a href="">1</a>
<a href="">2</a>
<a >3</a>
<div>div</div>
<script>
    $("[href]").css("background","red");
</script>
```

![image-20240627192157051](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240627192157051.png)

\$("[href='#']") 选中 href属性等于 # 的元素

```html
<a href="">1</a>
<a href="#">2</a><a >3</a>
<div>div</div>
<body>
<script>
    $("[href='#']").css("background","red");
</script>
```

![image-20240627192340016](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240627192340016.png)

\$("[href!='#']") 选中href不等于#的元素

```html
<a href="">1</a>
<a href="#">2</a>
<a >3</a>
<div>div</div>
<body>
<script>
    $("[href!='#']").css("background","red");
</script>
```

![image-20240627192429444](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240627192429444.png)
除了2 全红了！

**要是想选择多个属性怎么办？**
\$("\[属性1]\[属性2]")
\$("a\[href='#']\[title='abc']") 选中 href=# title=abc  的 a 元素

```html
<a href="">1</a>
<a href="#" title="abc">2</a>
<a >3</a>
<div>div</div>
<body>
<script>
    $("[href='#'][title='abc']").css("background","red");
</script>
```

![image-20240627192835192](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240627192835192.png)

### 表单选择器

1. 表单类型选择器

   ```
   <form>
       <input type="text"><br>
       <input type="password"><br>
       <input type="file"><br>
       <input type="button" value="按钮"><br>
       <input type="submit" value="提交按钮"><br>
       <input type="reset" value="重置按钮"><br>
   </form>
   ```

   ```
   $('input:text').css('background', 'red');
   $('input:password').css('background', 'red');
   $('input:file').css('background', 'red');
   $('input:button').css('background', 'red');
   $('input:submit').css('background', 'red');
   $('input:reset').css('background', 'red');
   ```

2. 表单状态选择器

   ```
   <form>
       <input type="text" autofocus><br>
       <input type="checkbox" checked>复选框<br>
       <input type="radio" disabled>单选框<br>
       <select>
           <option selected>列表项1</option>
           <option>列表项2</option>
       </select>
   </form>
   ```

   ```
   console.log($(':focus')[0]);
   console.log($(':checked')[0]);
   console.log($(':disabled')[0]);
   console.log($(':selected')[0]);
   ```

### **伪类选择器**

伪类选择器，顾名思义，是一种特殊的选择器，它用来选择DOM元素在特定状态下的样式。
这些特定状态并不是由文档结构决定的，而是由用户行为（如点击、悬停）或元素的状态（如被访问、被禁用）来定义的。
伪类名称对大小写不敏感
**动态伪类选择器**

1) **:hover** 当鼠标悬停在元素上时的样式
   代码示例：将链接的文本颜色改为红色

   ```css
   a:hover {
     color: red;
   }
   ```

2) **:active：** 当元素被用户激活（如点击）时的样式

   代码示例：将按钮的背景色改为蓝色

   ```css
   button:active {
     background-color: blue;
   }
   ```

3) **:focus：** 当元素获得焦点（如输入框被点击）时的样式。

   代码示例：将输入框的边框颜色改为绿色

   ```css
   input:focus {
     border-color: green;
   }
   ```

4) **:visited：** 用于设置已访问链接的样式，通常与:link一起使用来区分未访问和已访问的链接。

   代码示例：将已访问链接的颜色改为紫色

   ```css
   a:visited {
     color: purple;
   }
   ```

**UI元素状态伪类选择器**

1. **enabled和:disabled：** 用于表单元素，表示元素是否可用。

   示例：将禁用的输入框的边框颜色改为灰色

   ```css
   input:disabled {
     border-color: gray;
   }
   ```

2. **:checked：** 用于单选框或复选框，表示元素是否被选中。

   示例：将选中的单选框的背景色改为黄色

   ```css
   input[type="radio"]:checked {
     background-color: yellow;
   }
   ```

3. **:nth-child(n)：** 选取父元素中第n个子元素。

   示例：将列表中的奇数位置的项目的背景色改为蓝色

   ```css
   li:nth-child(odd) {
     background-color: blue;
   }
   ```

**否定伪类选择器**

1. **:not(selector)：** 选取不符合括号内选择器的所有元素。
   示例：将不是段落的元素的背景色改为灰色

   ```css
   *:not(p) {
     background-color: gray;
   }
   ```

| 选择器    | 例子           | 选择对象                                                     |
| --------- | -------------- | ------------------------------------------------------------ |
| :input    | $(":input")    | 选中所有表单元素!<br />表单元素包括 input,button,select,textarea... |
| :text     | $(":text")     | 所有type=text的input元素                                     |
| :password | $(":password") | type=password的元素                                          |
| :radio    |                | type=radio的元素                                             |
| :button   |                | type=button的                                                |
| :checkbox |                | type=checkbox的                                              |
| :submit   |                | type=submit的                                                |
| :reset    |                | type=reset的                                                 |
| :image    |                | type=image的                                                 |

1. 获取name属性值为 username的input元素
   $("input[name=username]")

2. 获取name属性值为courses且被选中的元素
   $("input[name=courses]:checked")

3. 当获取多个对象时，返回的是jQuery对象，而非js数组
   可在事件回调函数中直接使用jquery对象，但使用this时不能用箭头函数
   $("input[name=courses]").onclick(funciton(){$(this).hide()})
   当这个元素👆被点击时，这个元素调用回调函数，hide

4. 使ul下的li偶数变红

   ```html
   <ul class="content">
       <li>paragraph1</li>
       <li>paragraph2</li>
       <li>paragraph3</li>
       <li>paragraph4</li>
   </ul>
   <script>
           $("ul>li:odd").css("background","red");
   </script>
   ```

   为什么用odd？不是偶数even吗？even从0开始计数，它们好像是用index来的，第一行的index是0反倒是渲染出来odd成偶数了

## jQuery Event

jQuery也有自己的事件

| Mouse      | Keyboard | Form   | Document |
| ---------- | -------- | ------ | -------- |
| click      | keypress | submit | load     |
| dblclick   | keydown  | change | resize   |
| mouseenter | keyup    | focus  | scroll   |
| mouseleave |          | blur   | unload   |

将箭头函数作为参数注入这些事件中
**事件绑定**

.hover方法是两个回调函数的结合体：mouseenter和mouseleave
$("").hover(function(){},function(){});当mouseenter时，第一个函数启动！当mouseleave时，第二个函数启动！

```html
$("ul").hover(function(){$(this).text("you entered ul")},function(){$(this).text("you leave the ul")});
```

当悬浮在ul元素上时，ul元素的文本变成 you entered ul  离开后 ul文本变成 you leave the ul  反正是变不回一开始的了

当一个元素需要监听多个事件时，可以用on()方法同时注册
页面初始化时不存在而是在后期添加的元素，这些元素的监听必须使用on注册 

```html
 $("#p3").on({
            click:function (){
                $(this).text("click");
            },
            mouseenter:function (){
                $(this).text("mouseenter");
            },
            mouseleave:function (){
                $(this).text("mouseleave")
            }
        });
on里面一个大括号{click:绑定函数，mouseenter:绑定函数,mouseleave:绑定函数}
```



事件绑定后发生的东西都是回调函数
回调函数callback可以用 箭头函数作参数，也可以用函数做参数

```
    $("#reset").click(function (){
        $("#list").empty();
    });
    $("#reset").click(()=>{
        $("#list").empty();
    });
```

## 工具

### Get/Set

获得元素后可以使用这些方法，这些方法 **没参数时是 get  有参数时 是set**

| Method | Description                   |
| ------ | ----------------------------- |
| text() | 获取/设置文本                 |
| html() | 获取/设置html代码             |
| val()  | 获取/设置input元素的value属性 |
| prop() | 获取/设置元素的属性（可指定） |

```html
<p id="p3">aaaaaaaaa</p>
<button id="get">get</button>
<button id="set">set</button>
</body>
<script>
        $("ul").hover(function(){$(this).text("you entered ul")},function(){$(this).text("you leave the ul")});
        $("#get").click(()=>{
            alert($("#p3").text());
        });
        $("#set").click(()=>{
            $("#p3").text("set");
        })
</script>
```

**val()**
`.val()` 方法是 jQuery 提供的一个用于获取或设置表单元素值的方法。它不仅适用于 `<input>` 元素，还适用于 `<textarea>` 和 `<select>` 元素。

- **当用于获取值时**，`.val()` 方法没有参数，它返回被选元素的当前值。如果选择器匹配多个元素，它会返回第一个匹配元素的值。

```javascript
// 获取输入框的值
var username = $("input[name='username']").val();

// 获取文本域的值
var message = $("textarea[name='message']").val();

// 获取下拉框的选中值
var selectedOption = $("select[name='city']").val();
```

- **当用于设置值时**，`.val(value)` 方法接受一个参数 `value`，这个参数表示要设置的新值。它会将所有匹配的元素的值设置为指定的值。

```javascript
// 设置输入框的值
$("input[name='username']").val("John Doe");

// 设置文本域的值
$("textarea[name='message']").val("Hello, world!");

// 设置下拉框的选中值
$("select[name='city']").val("New York");
```

- 对于单选框和复选框，`.val()` 方法获取的是它们 `value` 属性的值

**prop（）**
prop有两种情况
一个参数是get某个属性的值
两个参数是修改第一个参数:属性的值 为 第二个参数

```
$("#set").click(()=>{
            let input=$("#p3");
            console.log(input.prop("type"));//一个参数，获得该元素的type属性值
            input.prop("type","checkbox");//两个参数，修改该元素type属性的值为checkbox
            console.log(input.prop("type"));//再获得一次
        })
```

![image-20240624191957271](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240624191957271.png)![image-20240624192008865](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240624192008865.png)

### Add

| 方法           | 效果                               |
| -------------- | ---------------------------------- |
| 元素.append()  | 在指定元素内部的结尾添加内容       |
| 元素.prepend() | 在指定元素内部的头部添加内容       |
| 元素.after()   | 在指定元素后添加内容，与该元素平级 |
| 元素.before()  | 在指定元素前添加内容，与该元素平级 |

```html
<body>
<p id="p1">this is a paragraph1</p>
<p id="p2">this is paragraph2</p>
<button id="btn">button</button>
</body>
<script>
    $("#btn").click(()=>{
        $("#p1").append("<b>append</b>");
        $("#p2").before("<p>this is paragraph3</p>");
    });
</script>
```

![image-20240625101504325](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240625101504325.png)

![image-20240625101519653](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240625101519653.png)



### Remove

| 方法                      | 效果                                             |
| ------------------------- | ------------------------------------------------ |
| 元素.remove([*selector*]) | 移除元素及其子元素<br />(可以用选择器指定子元素) |
| 元素.empty()(不接受参数)  | 移除元素的子元素                                 |

- **remove()**
  不带参数时，会移除指定的元素及其子元素
  且是直接从DOM文档中删，后续不能再使用该元素进行添加删除方法

  参数可以是选择器
  带参数时，只会移除该元素下匹配该选择器的节点，而其他的不删除

  ```
  $("#p").remove(".test,.demo")移除p元素下的 test和demo类元素
  ```

- **empty()**

  不接受参数
  清空节点的内容
  DOM文档中该节点仍然存在，后续可通过该节点增加删除内容

### Hide/Show

我们可以隐藏/显式 html元素通过方法 hide 和 show

$(selector).hide(speed,callback);

$(selector).show(speed,callback);

speed代表隐藏/显式的速度，callback是回调函数

方法toggle可以自动在 hide和show之间切换，不用再专门点show和hide了

$(selector).toggle(speed,callback);



speed可以是 "fast"  也可以是 "slow"  也可以是数字，代表毫秒

```html
		<div id="hs">变换元素</div>  
<script>
		$("#hide").click(()=>{
        $("#hs").hide();
        });//不写时间参数
        $("#hide2").click(()=>{
            $("#hs").hide(1000);
        });//写时间参数（毫秒）渐变
        $("#show").click(()=>{
            $("#hs").show();
        });
        $("#show2").click(()=>{
            $("#hs").show(1000);
        });
        $("#toggle").click(()=>{//点击toggle在两者之间自动转换
            $("#hs").toggle(1000,function (){
                $(this).text("toggle");
            })
        });
</script>
```

![hs](E:/PS/08stu/Web/hs.gif)

### Fading

渐入渐出效果

\$(Selector).fadeIn(*speed,callback*);渐入
\$(Selector).fadeOut(*speed,callback*);渐出
\$(Selector).fadeToggle(speed,callback);两者切换
\$(Selector).fadeTo(speed,opacity,callback);这个需要一个参数：透明度

```html
<body>
<button id="fadein">fadein</button>
<button id="fadeout">fadeout</button>
<button id="fadetoggle">fadetoggle</button>
<button id="fadeto">fadeto</button>
<div id="fade1" style="width:80px;height: 80px;background:red;"></div>
<div id="fade2" style="width:80px;height: 80px;background:orange;"></div>
<div id="fade3" style="width:80px;height: 80px;background:blue;"></div>
</body>
<script>
    $("#fadein").click(()=>{/渐入 出现
        $("#fade1").fadeIn();
        $("#fade2").fadeIn("slow");
        $("#fade3").fadeIn(3000);
    });
    $("#fadeout").click(()=>{/渐出 消失
        $("#fade1").fadeOut();
        $("#fade2").fadeOut("slow");
        $("#fade3").fadeOut(3000);
    });
    $("#fadetoggle").click(()=>{
        $("#fade1").fadeToggle();
        $("#fade2").fadeToggle("slow");
        $("#fade3").fadeToggle(3000);
    });
    $("#fadeto").click(()=>{
        $("#fade1").fadeTo("slow",0.15);
        $("#fade2").fadeTo("slow",0.3);
        $("#fade3").fadeTo("slow",0.7);
    });
```

![fade](E:/PS/08stu/Web/fade.gif)



### Sliding

滑动效果
\$(Selector).slideDown() 下滑
\$(Selector).slideUp() 上滑
\$(Selector).slideToggle() 转换

```html
<body>
<div id="flip">click to slide the panel down or up</div>
<div id="panel">Hello World!</div>
</body>
<script>
    $("#flip").click(()=>{
        $("#panel").slideToggle("slow");
    });
</script>
```

😓想用jQuery要先引入啊，不引入怎么用
![image-20240624200728931](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240624200728931.png)
![image-20240624200735316](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240624200735316.png)
点击后下滑出来，再点就滑回去
如果两者之间有东西,那么它就会在这个东西的下面滑出来，如果这个东西在滑动东西的下面，则在滑出来时它被顶走

```html
<div id="flip">click to slide the panel down or up</div>
aaa
<div id="panel">Hello World!</div>
```

### Css

| 方法          | 效果              |
| ------------- | ----------------- |
| addClass()    | 给元素增加类      |
| removeClass() | 删减类            |
| toggleClass() | 点击增加再点删减  |
| css()         | 设置元素的CSS属性 |

**addClass()**
`addClass()` 方法用于向匹配的元素添加一个或多个类

```html
// 添加一个类名
$("#myElement").addClass("highlight");

// 添加多个类名，使用空格分隔
$("#myElement").addClass("highlight important");
```

**removeClass()**
`removeClass()` 方法用于从匹配的元素中移除一个或多个类。

```
// 移除一个类名
$("#myElement").removeClass("highlight");

// 移除多个类名，使用空格分隔
$("#myElement").removeClass("highlight important");
```

**toggleClass()**
`toggleClass()` 方法用于在匹配的元素上切换一个或多个类。如果元素已经有指定的类，则移除它；如果元素没有该类，则添加它。

```
// 切换一个类名
$("#myElement").toggleClass("active");

// 切换多个类名，使用空格分隔
$("#myElement").toggleClass("active highlight");

// 可以提供一个布尔值作为第二个参数来强制添加或移除类
$("#myElement").toggleClass("active", true); // 强制添加类名
$("#myElement").toggleClass("active", false); // 强制移除类名
```

**css()**
`css()` 方法用于获取或设置匹配元素的样式属性值
它可以用于读取元素的CSS样式属性，也可以用于设置一个或多个CSS样式属性的值。

1. **获取样式属性值**

   通过传入一个样式属性名称，可以获取匹配元素的该样式属性的当前值。

   ```
   // 获取id为myElement的元素的背景颜色
   var bgColor = $("#myElement").css("background-color");
   console.log(bgColor); // 输出当前背景颜色值
   ```

2. **设置样式属性值**

   ```
   // 设置id为myElement的元素的背景颜色为红色
   $("#myElement").css("background-color", "red");
   ```

3. **设置多个样式属性值**

   ```
   // 设置id为myElement的元素的背景颜色和字体大小
   $("#myElement").css({
       "background-color": "blue",
       "font-size": "16px"
   });
   ```

### Chaining

jQuery的元素也可以链操作
$("#p1").css("color","red).slideUp(2000).slideDown(2000);

| 方法       | 效果                 |
| ---------- | -------------------- |
| filter()   | 过滤符合的           |
| not()      | 过滤不符合的         |
| children() | 在子元素中查询       |
| find()     | 在全部后代中查询     |
| parent()   | 在父元素中查询       |
| parents()  | 在全部祖先元素中查询 |
| next()     | 平级的下一个元素     |

filter和not里面放的是也是 \$("selector")，在调用方法的 jQuery 集合里 过滤后者  实验四中去除掉提交按钮

```javascript
 $("#register :input").not($("button[type=submit]"))
选中了 id=register元素下的所有表单元素，然后剔除 $("button[type=submit]")这个元素
该语句代表上述操作后剩下的元素
实验四就通过这个选中了所有表单元素
```





## 需求

**需求: 将输入框中的内容动态以渐入效果追加至列表**

```html
<p>淡入效果，输入内容追加至列表</p>
<input id="input"><button id="btn">追加</button>
<ol id="list">
</ol>
<script>
    $("#btn").click(()=>{
        let input=$("#input");//获取input对象
        let context=input.val();//获取input输入框的值,输入框 tyue=text 那么返回字符串
            input.val("");//清空输入框
        if(context===""){}//JS判断字符串是否相等不用equals方法，而是直接 ===
        else{
            let newitem = $(`<li>${context}</li>`);//创建对象，用来添加
            newitem.css("display", "none");//隐藏该对象，即使添加进入了列表也隐藏
            $("#list").append(newitem);//添加
            newitem.fadeIn(2000);//前面隐藏了，现在渐入显示
            }
    });
</script>
```

**需求：用户仅能选择指定数量的选项**

```html
<label><input type="checkbox" name="course">java</label><br>
<label><input type="checkbox" name="course">web</label><br>
<label><input type="checkbox" name="course">c++</label><br>
<script>
    const amount=2; //预设最大选择数量
    const checkboxs=$("input[name=course]");//获取一组对象，返回对象数组
    checkboxs.click(()=>{//当数组中的任何一个被点击时
        //检查目前checked的数量，如果不小于amount 那么num为true
        let num=checkboxs.filter(":checked").length >=amount;
        //选中未被checked的复选框，使其disabled属性为 true 便无法选中
        checkboxs.not(":checked").prop("disabled",num);
    })
</script>
```



# Servlet

## What's Servlet

1. 是技术！是API！是接口！是类！是Web的好伙伴！

2. Web容器创建线程用来承载，运行web应用
   现在我们用Tomcat作为这个Web容器
   接收请求并做处理
   Tomcat帮我们把请求转发到可以处理该请求的服务器
   全部由 Tomcat完成

3. Orcale开源java EE后 社区不让用Java EE命名，在此之后以用Jakarta EE
   之前的项目 引用的包的名字都是javaEE,放在现在就用不了了
   因为JavaEE已经被禁用了。
   把JavaEE改为Jakarta EE便可使用
   在maven配置中，声明servlet依赖时也要注意是jakartaEE
   <img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612204828954.png" alt="image-20240612204828954" />

   原来的javaEE已经不好用了
   ![image-20240612204909406](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612204909406.png)

4. 关于项目的构建形式
   war exploded
   项目编译后，构建为文件夹，部署到服务器
   war
   项目编译后，构建为web项目的war包，部署到服务器；
   Tomcat服务器自动解压为文件夹
   即无论怎样构建，tomcat均按文件夹部署项目(并非所有服务器均需解压)

## Servlet

是一个接口
jakarta.servlet.Servlet接口
主要定义了三个servlet生命周期回调方法
1.<font color = blue>init() </font>
2.<font color = blue>service(ServletRequest request，ServletResponse response) </font>
3.<font color = blue>destory()</font>

当Servlet第一次被创建时，容器回调init()方法
执行初始化资源等操作。容器创建servlet对象后回调，只回调一次

当Servlet关闭时，容器回调destory(方法）
执行资源释放等操作，容器销毁servlet对象前回调，只回调一次

每次servlet请求，容器均回调service()
可以处理多个并发请求，线程安全，每次请求都回调一次
将请求转发至具体方法处理

> 容器指的是 Web容器，在这里是 Tomcat



## HttpServlet

### Servlet类

<font color=229453>如何处理servlet请求？使用servlet类对具体请求具体处理</font>

如何创建servlet类？
创建类，该类继承自HttpServlet接口

```
public Myservlet extends HttpServlet{

}
```

<font color=229453>那么创建了类之后，这个类具体处理哪个路径的请求呢？</font>
<font color = blue>用@WebServlet(value)注解</font>
常用的写法是将 Servlet 的相对请求路径（即 value）直接写在注解内

```
@WebServlet("/hello")
public Myservlet extends HttpServlet{
}
在这种情况下，我们对该项目的hello资源访问时
便由这个类来接待我们处理我们的请求
```

<font color = blue>**`value`**</font>声明处理的请求地址
容器启动后时会扫描所有@WebServlet注解的类，基于属性配置创建servlet实例

<font color=229453>@WebServlet("/hello")</font>

/ 根为项目根路径，而非服务器根路径
如果没有 / 根，则会当前路径的相对请求

/hello便是该类处理 访问该路径的请求

<font color=229453>处理请求地址与其源文件所在包目录及名称无关</font>
<font color=229453>这个hello不一定是项目里的资源</font>
<font color=229453>它只代表当我们对该路径请求时，服务器将调用注解了这个地址的Servlet类</font>
![image-20240612225325626](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612225325626.png)

我们的项目里并没有 123456这个资源，但是声明了这个之后
我们访问 服务器+部署地址+123456
http://localhost:8080/Web/123456
此时不会因为资源不存在而404，而是服务器调用这个类，这个类给一个响应resp
![image-20240612225446639](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612225446639.png)

<font color=229453>当项目里资源，与Servlet类注解处理地址重名时，会优先调用Servlet类，而不是这个静态资源</font>

### Logging

<font color=229453>Log(日志) 记录应用运行的时间信息，日志信息打印在控制台里</font>
<font color=229453>日志的 `System.out`输出不具可维护性,所以日志输出在控制台</font>

java.util.logging.Logger java提供的简单的日志工具

<font color = blue>`Logger.getLogger()`返回一个Logger对象</font>

<font color = blue>Logger.getLogger(String name)</font>

<font color=229453>接受一个字符串参数`name`</font>
<font color=229453>这个参数通常是要记录日志的类的全名。</font>
<font color=229453>这个方法返回一个与给定名字关联的`Logger`对象</font>
name乱写没用，乱写无效，乱写输出的还是该类的全名
![image-20240612223104888](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612223104888.png)

![image-20240612223129536](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612223129536.png)

奇了怪了，好像输入什么都是输出对象所在类的全名,那就这么记吧

<font color = blue>Logger.getLogger(Class<?> clazz)</font>
<font color=229453>这个方法接受一个Class类型的参数`clazz`</font>
<font color=229453>这个参数通常是要记录日志的类的类对象</font>
目前不用第二个

<font color = blue>实例方法 .info(string)</font>
<font color=229453>接受一个字符串参数，这个参数是想要额外记录的日志信息。 不能放空，空字符用""</font>
<font color=229453>当调用这个方法时，它会将这个信息添加到调用该方法的日志对象中。</font>

效果：
<font color=229453>在控制台上输出 </font>
<font color=229453>创建日志时传入的name+该对象调用info方法时所在的方法名+info新加的信息</font>
如在方法 doGet里调用 info方法，输出结果为  Hello.doGet infoString
![image-20240612223348443](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612223348443.png)
![image-20240612223356796](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240612223356796.png)



```java
@WebServlet("/hello.html")
那么访问项目/hello.html资源时便会由该Servlet类处理
public class Hello extends HttpServlet {
    private static final Logger LOGGER=
            Logger.getLogger(HttpServlet.class.getName());
//定义日志对象，该对象的内容↑  先记住这个定式
    @Override
    public void init(ServletConfig config) throws ServletException {//回调init时 info
        super.init(config);
        LOGGER.info("init");
    }

    @Override
    protected void service(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        super.service(req, resp);
        LOGGER.info("service");
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        LOGGER.info("doGet");
    }
}
```

### ServletRequest & HttpServletRequest

后者继承自前者，两者都是接口
Servlet容器 创建请求(request)/响应对象(response)。封装他们的数据信息，<font color=229453>将 **请求/响应对象** 作为参数注入方法</font>

> 当部署服务器后，我们访问资源时，我们的访问是Get
> 由Servlet类中的doGet方法处理,我们的访问就是调用了doGet方法
> 本来有资源的网页却是白屏，不是404说明找到了资源，但是没有内容
> 这是因为我们对某地址发出get请求，收到什么回应取决于doGet()的处理方法
> 如果doGet()什么都不做，那就什么也没有，白屏

####  如何传值？

URL  GET请求，基于 键值对 传递参数
允许为同一参数指定不同的参数值，Servlet按数组接收
传递非ASCII字符时需按照16进制编码（浏览器自动实现，不用担心）
<font color = red> 严禁基于get请求传递的参数修改数据库数据</font>

<font color = red>HTTP协议仅支持传递字符串，需手动完成类型转换！</font>

1. <a href="/Web/hello?id=1&name=david>链接</a\>
   href="访问地址"， 访问地址后用问号隔开，后面是参数
   参数以键值对的形式传递，以上点击后传入两个参数  不同参数间用 & 连接
   1 key=id , value=1   2. key=name value="david"
   **！**第二个参数值不对！HTTP仅支持传递字符串，什么意思？他会把所有的值当作字符串传过去！所以字符串不要加双引号

   这个路径是向服务器发起的请求， /是服务器根，所以正确写法: /Web/hello
   a超链接传值属于 GET 请求  点击这个链接就等于对这个地址发出了GET请求

2. form表单传值

   ```http
   <form action="/Web/hello" method=post>
   <input name="username"><br>
   <input name="password" type="password"> <br>
   <button type="submit">login<button>
   </form>
   ```

   1. form action属性值代表请求地址
   2. form method默认为GET，POST请求要修改为post
   3. form表单最终向提交要使用 type="submit" 的button

   效果：用户在两个输入栏里输入的值作为 这两个键的值传过去
   如果没输入值，就不传；想不输入也传值？主动给键弄一个值
   \<input name="password"  value="不输入也传进去的值" type="password"> 

<font color = red>**无论是 a 超链接跳转 还是 form 表单提交，都是客户端发出的请求，因此两者的路径中   /  都代表服务器根地址**</font>

实例方法
<font color = blue>String getParameter(String name)</font>
<font color = blue>数组 getParameterValues(String name)</font>

<font color = blue>获取get/post请求中传递的参数</font>
这个name需要跟键一模一样才能取值

```java
<a href="/Web/hello?id=1&name=David">链接！</a>
我在一个网页里放进了这个超链接，它会向 项目hello地址发出get请求并且带上两个参数
那么该网页的Servlet类怎么取值？
@WebServlet("/hello")
public class Hello extends HttpServlet {
    private static final Logger LOGGER= Logger.getLogger(HttpServlet.class.getName());//日志文件
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        resp.getWriter().write(req.getParameter("id"));//取值，看到没？参数要是传入参数的键
        LOGGER.info("doGet");
    }
}
参数是在请求里的 req 里的 所以这个方法是 req 的静态方法
req.getParameter("id")-> 1
req.getParameter("name")->David
这两个值都是字符串啊，http只让传字符串，想让1当整形使，手动类型转换
```

```java
form表单传值------一口气全搞完！
<form action="/Web/hello" method="post">
        Username: <input name="username"><br>  
        Password: <input name="password" type="password"><br>
        两个输入框，输入的值作为这两个键的值传过去
        Degree:   
        <select name="degree">
        <option value="1">学士</option>
        <option value="2">硕士</option>
        <option value="3">博士</option>
   		</select><br>
		一个select 选中的option的value作为select键的值传过去
        
        <input type="checkbox" name="course" value="111">Web
        <input type="checkbox" name="course" value="111">Java
		两个checkbox 对应同一个键，全选了怎么办？怎么对这个键取值？会覆盖吗？
		不会新的覆盖旧的，这两个值作为数组当作 course的值传了过去
		用 getParameterValues 取值，返回数组
       <br> <button type="submit">提交</button>
    </form>

@Override
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        LOGGER.info(req.getParameter("username"));
        LOGGER.info(req.getParameter("password"));
        LOGGER.info(req.getParameter("degree"));
        LOGGER.info(req.getParameterValues("course")[0]);//这里只取了数组的第一个，也就是web对应的value:111
    }
```

![image-20240613223233615](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240613223233615.png)![image-20240613223251237](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240613223251237.png)

#### Get Post

|                    | Get                                                          | Post                                                         |
| :----------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 点击返回/刷新      | 重新提交Get请求，没有影响                                    | 重新提交POST请求，数据会重复发送<br />这样不好，浏览器也会提示 |
| 请求地址添加书签？ | 可以                                                         | 不可以                                                       |
| 缓存？             | 可以                                                         | 不可以                                                       |
| 历史记录？         | 有                                                           | 没有                                                         |
| 长度限制           | 有，由服务器及浏览器决定                                     | 没有                                                         |
| 数据类型限制       | 只支持ASCII码                                                | 没有，允许二进制数据                                         |
| 安全性             | 查询字符串会限制在地址栏的URL中<br />即传的什么东西都能看见，所以不用GET提交敏感数据 | 不显示在地址栏，不会缓存，不会记录<br />但还是明文传递，敏感信息仍需加密 |
| 可见性             | 可以在地址栏看见                                             | 看不见，但是可以拦截                                         |



传值中文跟响应中文都是乱码，怎么解决？

response.setCharacterEnconding("UTF-8")放入请求处理方法里 设置浏览器编码格式
get请求就放入doGet里

#### Resp

如何给客户端响应一个网页？
可以用这种神奇的方式拼出一个html代码（记得先设置编码格式哦）
![image-20240613224400836](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240613224400836.png)

但这种方法看着就不太行对吧
实际不用这种方法



#### Sum

Servlet容器与Servlet接口规范单向耦合，Servlet应用与Servlet接口规范单向耦合，具体应用与具体容器，无任何耦合

从而使任何实现了Java Servlet规范的应用，可以部署到任何实现了Servlet规范的容器中；

使应用与容器解耦

无敌！



## 转发与定向

<font color = red>**转发是项目内部进行转发，因此转发的路径中 /  代表项目的根地址** </font>

### 转发

<font color=229453>有些资源封装起来，不让外部直接访问，那到底怎么访问呢？</font>
<font color=229453>既然不让直接访问，那我们就内部转发，转发到需要的资源那儿。我们虽然看到了资源，但是URL还是我们之前请求的地址</font>
<font color=229453>比如访问hello 然后hello Servlet类里有处理将Get请求转发到hello.html里,那么我们就能看到hello.html,但是地址栏的URL还是hello</font>
<font color=229453>意思是什么？意思是用户根本不知道自己的请求被转发到哪了</font>

项目的WEB-INF和META-INF是项目安全目录，外部无法直接访问这两个目录下的资源
思想：对外暴露请求路径，不对外暴露资源
如：我们客户端访问网址是/Web/hello，然后这个网址的Servlet类给我们转发到 /Web/hello.html去，而hello.html 隐藏s

实例方法
<font color = blue>req.getRequestDispatcher("转发目的地").forward(req,resp)</font>

获得对象并转发到目的地，怎么做到的？
这是项目内部转发，所以 / 代表项目根地址 
例子写法是  /WEB-INF/hello.html

<font color = blue>.forward(req,resp)</font>
是把用户最初的请求也一起转过去，这个并不是getResquestDispatcher的内容



<font color=red>**注意!**</font>
如果仅仅调用`getRequestDispatcher("/test.html")`而没有调用`.forward(req, resp)`，实际上没有进行转发操作
因此客户端将不会收到来自`/test.html`的任何响应内容,只会看到一个空白页面，因为没有响应啊。
`getRequestDispatcher()`仅获取了一个`RequestDispatcher`对象，但并未实际进行请求的转发。
**必须使用`.forward(req, resp)`进行转发**如果你希望通过转发将请求发送到另一个资源，并且希望客户端最终接收到该资源生成的响应内容，你必须调用`.forward(req, resp)`。这样Servlet容器才会将请求和响应传递给目标资源，目标资源处理请求并生成响应，最终将响应发送回客户端。




 实例应用：Login  Welcome 登录界面操作

1. 登录

   客户端对项目的login发出请求，login内部转发到不允许直接访问的login.html
   我们在login的Servlet类里 重写doGet 对该请求进行转发，转发到login.html里（内部转发）
   然后login.html里有登录表单，这个表单填写登录信息
   **表单信息如何提交？**
   
   1. 设置 \<input type="submit">
   2.  设置\<button type="submit">

   我们知道无论是 a 超链接跳转 还是 form 表单提交，都是客户端发出的请求，因此两者的路径中   /  都代表服务器根地址

   **表单的action代表提交到的地址**
   表单提交是客户端对服务器发出的请求，所以这里的 /是服务器的根，路径写法是：/Web(项目路径)/login
   **表单method代表对action路径的请求类型**
   默认get。如果不改，这次提交就是对 login发出get请求，Servlet类又使用doGet处理这次get请求，给我们转发会login.html界面
   所以我们要声明这是 post 请求  method=post，然后在 Servlet 类里重写doPost方法，验证账号密码，然后内部转发。
   
   ```html
   login.html
   <form action="/Web/login" method="post">
   //要点1：action 里 / 代表服务器根
   //要点2：注意method的值
       <span class="span input">Username</span> <input name="username">
       <span class="span input">Password</span> <input type="password" name="password">
       <button type="submit">登录</button>
   </form>
   //要点3：input,button要包在form里面！
   ```
   
   ```java
   @WebServlet("/login")
   public class LoginService extends HttpServlet {
       private static final Logger LOGGER= Logger.getLogger(HttpServlet.class.getName());
       @Override//重写doGet
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           req.getRequestDispatcher("/WEB-INF/login.html").forward(req,resp);
           LOGGER.info("login");
       }
   // 注意内部转发  / 代表项目路径
       @Override//重写doPost
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           LOGGER.info("welcome");
           if(req.getParameter("username").equals("pang")){
               req.getRequestDispatcher("/WEB-INF/welcome.html").forward(req,resp);
           }
       }
   }
   ```
   
   注意！
   项目部署完后，要手动把 login.html ,welcome.html放入WEB-INF文件夹中，修改后要重新放一遍

### 重定向

Redirect

重定向是让客户端再次发起一个请求
1.客户端向服务器发起一个请求
2.服务器执行重定向方法，响应给客户端，让客户端重新定向
3.客户端接收到服务器的响应resp，执行响应中的重定向要求
结果：客户端重新发起一个GET请求 能切仅能发起GET重新定向请求

实例方法
<font color = blue>**resp.sendRedirect("地址")**</font>
这是客户端发的请求，以 / 开头的话，/是服务器的根
想定哪儿定哪儿，也可以定到B站去resp.sendRedirect("http://www.bilibili.com");

```
@WebServlet("/re")
public class Redirect extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
    resp.sendRedirect(req.getContextPath()+"/hello.html");
    }
}/让客户端重新发起到 项目的login的请求
```

这是强制让客户端再发起一个GET请求，请求地址就是方法里写的地址
这个不是内部转发啊，重定向后，客户端浏览器地址栏里的URL也会变成那个地址的，转发不会变
重定向能明显看到被定到了哪儿去
![image-20240614151016470](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240614151016470.png)![image-20240614151109862](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240614151109862.png)

执行后：![image-20240614151125370](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240614151125370.png)

我们得到什么教训？通过字符串连接变成地址，记得手动加上 /
![image-20240614151204172](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240614151204172.png)



> <font color=red>req.getContextPath()</font>返回项目当前部署路径，客户端向服务器的re发出请求地址其实是服务器/部署地址/请求路径，该方法返回 服务器+部署地址
>
> 这里 服务器由  / 代表，/代表服务器根地址， 部署路径是Web 请求路径是re
> 那么这个方法就会返回 /Web 



应用-改进登录

1. ```java
   @WebServlet("/login")
   public class LoginService extends HttpServlet {
       private static final Logger LOGGER= Logger.getLogger(HttpServlet.class.getName());
       @Override
       protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           req.getRequestDispatcher("/WEB-INF/login.html").forward(req,resp);
           LOGGER.info("login");
       }
   
       @Override
       protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
           LOGGER.info("welcome");
           if(req.getParameter("username").equals("pang")){
               resp.sendRedirect(req.getContextPath()+"/welcome");
           }
           else{
               resp.sendRedirect(req.getContextPath()+"/login");
           }
       }
   }
   成功了，重定向到项目/welcome 发出GET请求，welcome Servlet类将该请求转发到welcome.html
   失败了，重定向到项目/login 再次发出GET请求
   不管成功与否，都重新定向，这样刷新时，不再是在提交那个页面刷新了，也就避免了重复提交数据
   ```

   



|                         Redirect                          |                 RequestDispatcher                  |
| :-------------------------------------------------------: | :------------------------------------------------: |
|                  response.sendRedirect()                  |        req.getRequestDispatcher().forward()        |
| 服务器通知客户端发起新的GET请求<br />地址栏变为重定向地址 | 服务器内部转发，与客户端无关<br />客户端地址栏不变 |
|                   产生新的req/resp对象                    |                 使用原req/resp对象                 |
|                         /服务器根                         |                      /项目根                       |
| 用于post请求的重复提交<br />无论post是否成功，都要重定向  |              用于转发资源而不暴露资源              |

## Scope

**Servlet Scope**作用域

- Servlet Scope
  **请求级** 生命周期与 HttpServletRequest对象绑定。当resquest对象销毁时生命周期结束。
  仅一次请求内有效，一次GET完就没了
  关闭页面销毁
- Session Scope
  **会话级** 生命周期与 HttpSession对象绑定，在用户的整个会话内有效 
  一次校验完成后一直有效，直到退出
  关闭浏览器销毁
- Application Scope
  **应用级** 生命周期与ServletContext对象绑定,在应用的整个生命周期内有效

三个作用域类型的接口
jakarta.servlet.http.HttpServletRequest
jakarta.servlet.http.HttpSession
jakarta.servlet.ServletContext

### Servlet Attributes

在请求里塞入键值对，那么可以随着键值对来回传递
键必须为String类型，值为任意类型的**对象**

每个作用域接口都包含setAttribute()/getAttribute()方法

<font color = blue>xxx.setAttribute(String name,Object o)</font>
name 键名  o  对象
在请求间传递对象，对象以字符串命名，组成键值对



<font color = blue>Object xxx.getAttribute(String name)</font>
name  键名，返回值: Object类型的对象
虽然键值对里值可以是任意类型的对象，但是取出来的时候是Object类型的，需要手动转换类型





### 作用域

1. 项目启动后第一次请求doGet  为三种对象全部设置值

   ```java
   req.setAttribute("request","request级作用域")
   HttpSession session=req.getSession();//req.getSession 获取 Session 对象
   session.setAttribute("session","session级作用域");//设置属性
   ServletContext context=req.getServletContext();//req.getServletContext 获取 Context 对象
   context.setAttribute("context","context级作用域");//设置属性
   get方法返回值是Object类型，手动转换为原类型
   LOGGER.info("第一次请求"+(String)req.getAttribute("request"));
   LOGGER.info("第一次请求"+(String)session.getAttribute("session"));
   LOGGER.info("第一次请求"+(String)context.getAttribute("context"));
   Hello.doGet 第一次请求request级作用域
   Hello.doGet 第一次请求session级作用域
   Hello.doGet 第一次请求context级作用域
   ```

   各作用域对象正常打印

2. 之后不再为三种对象设置值
   浏览器不关闭，项目不关闭，重新发起请求

   ```java
   HttpSession session=req.getSession();//req.getSession 获取 Session 对象
   ServletContext context=req.getServletContext();//req.getServletContext 获取 Context 对象
   LOGGER.info("第二次请求"+(String)req.getAttribute("request"));
   LOGGER.info("第二次请求"+(String)session.getAttribute("session"));
   LOGGER.info("第二次请求"+(String)context.getAttribute("context"));
   Hello.doGet 第二次请求null
   Hello.doGet 第二次请求session级作用域
   Hello.doGet 第二次请求context级作用域
   ```

   发出新的请求时，
   req 是否保存有上次请求设置的值？没有
   session对象是否保持？是
   context对象是否保持？是
   **request对象的作用域仅有一次请求，该请求结束，req销毁**

3. 浏览器关闭再打开,再发请求

   ```java
   HttpSession session=req.getSession();//不设值但是取对象，下面的打印需要一个session对象
   ServletContext context=req.getServletContext();
   LOGGER.info("第三次请求"+(String)req.getAttribute("request"));
   LOGGER.info("第三次请求"+(String)session.getAttribute("session"));
   LOGGER.info("第三次请求"+(String)context.getAttribute("context"));
   Hello.doGet 第三次请求null
   Hello.doGet 第三次请求null
   Hello.doGet context级作用域
   ```

   浏览器关闭，再发请求
   session值消失
   context值存在
   **session对象随浏览器关闭销毁** 

4. 项目关闭再启动，doGet

   ```java
   HttpSession session=req.getSession();
   ServletContext context=req.getServletContext();
   LOGGER.info("第四次请求"+(String)req.getAttribute("request"));
   LOGGER.info("第四次请求"+(String)session.getAttribute("session"));
   LOGGER.info("第四次请求"+(String)context.getAttribute("context"));
   Hello.doGet 第四次请求null
   Hello.doGet 第四次请求null
   Hello.doGet 第四次请求null
   ```

   全没了，context 作用域最长，整个项目运作时它都存在
   **context对象随项目关闭销毁**

### Cookie

Http协议不保存客户端与服务器的 互交状态
Cookie基于文本文件保存在客户端
Session基于唯一标识的字符串

客户端第一次请求后，服务端生成唯一标识（标识该客户），并发送回客户端
客户端再次请求时会在header中携带该标识，服务器验证该标识，验证客户端的身份

**Session对象的销毁（详细）**
1.浏览器关闭（非页面关闭）
2.服务器基于配置（Tomcat默认20分钟）清空没有请求的客户端
	Tomcat的话，即20分钟内没有人访问该session对象便销毁
3.服务器显式调用HttpSession.invalidate() 方法 显式销毁服务器的Session对象
4.服务器关闭重启等等

应用场景：保存登录用户角色/权限/id等基本信息

实操：用户登录失败返回login页面，成功跳转到welcome界面；只有用户登陆后可以访问welcome，直接访问的话跳到login页面

```java
public class User {//封装用户信息
    private String name;
    private LocalTime localTime;
    public User(String name,LocalTime localTime){
        this.name=name;
        this.localTime=localTime;
    }
}
public class DatabaseUtils {//验证信息，正确就封装用户名和登录时间
    public static User getUser(String userName,String passWord){
        User user=null;
        if(userName.equals("pang")&&passWord.equals("123")){
            user = new User("Pang", LocalTime.now());
        }
        return user;
    }
}
```

```java
@WebServlet("/login")
public class LoginService extends HttpServlet {
    private static final Logger LOGGER= Logger.getLogger(HttpServlet.class.getName());
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        req.getRequestDispatcher("/WEB-INF/login.html").forward(req,resp);
    }//转发登录页面

    @Override
   protected void doPost(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        String userName=req.getParameter("username");
        String passWord=req.getParameter("password");
		User user = DatabaseUtils.getUser(userName,passWord);
        String url
        if(user!=null){//验证，通过就转到welcome
            req.getSession().setAttribute("user",user);  //第一次请求，用户合法便将用户信息添加至session
            url="/welcome.html";
        }
        else{//失败就重新登录
            url="/login";
    }
        resp.sendRedirect(req.getContextPath()+url);//成功与否都重定向
    }
}
```

```java
@WebServlet("/welcome")
public class WelcomeService extends HttpServlet {
    @Override//在上面的逻辑中，如果成功登录，对象会传入Session里，所以这里通过取Session的对象来验证是否成功登录，如果Session对象里没键，就是未登录
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
       User user= (User) req.getSession().getAttribute("user");
       if(user!=null){
           req.getRequestDispatcher("/WEB-INF/welcome.html").forward(req,resp);
       }
       else{
           resp.sendRedirect(req.getContextPath()+"/login");
       }
    }
}
```

首次请求时，客户端的Header里没有cookie属性，如果客户端这次调用了session，服务器便自动生成cookie通过resp传给客户端
然后客户端在本地以cookie为键放入session对象。
以后该客户端发起请求时，服务器以客户端中header中的cookie为键找到对性的session对象
客户端在有了cookie后自动带上cookie不需要手动在header里添加
达成服务器保存客户信息

简要：客户端发出请求->服务器生成session并给客户端一个cookie同时以cookie为键存储客户信息放入session->
客户端以后带着cookie来，服务器根据cookie找到对应的session

|                           Cookie                           |        Session         |
| :--------------------------------------------------------: | :--------------------: |
|                      数据保存在客户端                      |   数据保存在服务器端   |
|                       只能村ASCII码                        |      直接保存对象      |
|                 可以设置失效时长，长期有效                 |        短期有效        |
|                      不占用服务器资源                      |       服务器维护       |
|                     单cookie文件限制4k                     |         无限制         |
|                       支持跨域名访问                       |         不支持         |
| 数据应加密后保存<br />因为放在本地是个文本文件，打开就能看 | 客户端不可见，无需加密 |

基于256bits PBKDF2对称算法，加密用户数据保存在cookie中，这样虽然在本地，但是看不懂

### Header

HTTP的 请求(req)/响应(resp)中默认包含header 封装了 类型/编码/长度/主机/端口/请求来源/cookie/SessionID等信息
可以遍历查看

```java
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        Enumeration head=req.getHeaderNames();
        while(head.hasMoreElements()){
            String paramName=(String) head.nextElement();
            String paramValue=req.getHeader(paramName);
            System.out.println(paramName+":"+paramValue);
        }
    }
```

### 状态码

| 代码 | 消息                  | 描述                                      |
| ---- | --------------------- | ----------------------------------------- |
| 200  | OK                    | 请求成功                                  |
| 302  | redirect              | 重定向                                    |
| 400  | Bad Request           | 请求错误                                  |
| 404  | Not Found             | 请求资源不存在                            |
| 500  | Internal Server Error | 未完成请求 服务器遇到意外                 |
| 502  | Bad Gateway           | 未完成请求 服务器从上游服务器收到无效响应 |
| 503  | Service Unavailable   | 未完成请求 服务器暂时超载或者死机         |

4开头时客户端的问题，这些返回的消息可以自定义

### 传输

在非加密的HTTP请求中，post请求数据未在地址栏显示，但是form表单数据在请求体中以明文传递
因此，基于HTTP协议的传输数据可以被拦截监听，不安全
用HTTPS协议来传比较安全

传中文不是直接传，浏览器自动编码传过去，最后用的时候再解码

## Filter

过滤器
过滤器可以用来过滤，也可以用来对所有的请求进行一层操作
若干过滤器是相连的，请求进来的时候过一遍过滤器，离开的时候也得挨个过一遍过滤器

### 三种匹配方式

1. 精准匹配
   /user/LoginServiet
   仅过滤指定路径地址的请求
2. 路径匹配
   /admin/*
   通配符*，过滤指定路径下的所有请求
3. 扩展名匹配
   *.action
   过滤指定后缀扩展名的所有请求
4. 不支持扩展名匹配和路径匹配结合
   /admin/*action 错！

### 声明创建

@WebFilter注解+继承 HttpFilter类
类里重写doFilter方法进行具体操作

```java
@WebFilter("/*")
public class MyFilter extends HttpFilter{
对项目下的所有请求都拦截
@Override
protected void doFilter(HttpServletRequest req,
                       HttpServletResponse resp,
                       FilterChain chain) throw ···{
    req.
	resp.
	chain.doFilter(req,resp);
}
}
```

若干个过滤器就是漏斗
doFilter里的 chain.doFilter就是漏斗口
chain对象调用这个方法，就是允许接着传下去，传到哪儿咱也不知道，反正是传出去了，直到资源
不调用这个方法就是传不动了，过滤链到此为止。传不到资源处

### 实例



```java
@WebFilter("/*")//拦截项目下的所有请求
public class LoginFilter extends HttpFilter {
    private List<String> excludes= List.of("/login");//excludes代表允许放行的请求，这里只写了login
    @Override
    protected void doFilter(HttpServletRequest req, HttpServletResponse resp, FilterChain chain) throws ServletException, IOException{
    for(String e:excludes){//如果该请求允许直接放行，那么我们就调用chain.doFilter放过去
        if(e.equals(req.getServletPath())){
            chain.doFilter(req,resp);
            return;
        }
    }
    //如果这个请求不在直接放行里，单独处理，什么都不处理就是不允许放行
	//我们这里看用户是否为登录状态作为处理标准，如果用户登陆了，随意访问，未登录就让他们登录去
    User user=(User)req.getSession().getAttribute("user");
    if(user!=null){
        chain.doFilter(req,resp);
    }
    else{
        resp.sendRedirect(req.getContextPath()+"/login");
    }
    }
}
```

### 注意

所有涉及到URL的元素，无论是图片、视频还是其他资源，浏览器在加载页面都会向声明的url地址发起请求。
这些请求由浏览器根据页面中的资源路径发起，如果这些资源路径指向了项目内的资源，例如 `/resource/img/foot.jpg`，那么浏览器会向这个路径发送请求，以获取相应的资源文件。既然是向项目内部发起的请求，这意味着这个请求可能被过滤器拦截

如果你在项目中配置了一个过滤器 (`/*`)，这意味着它会拦截所有进入应用的请求。这包括所有类型的请求，包括HTML页面、CSS文件、JavaScript文件、图片、视频等等。假如浏览器向项目内部的图片资源发起请求，但是被拦截了，就会导致图片加载不出来，这也是之前设置了过滤器后图片消失的原因

对于图片和其他静态资源，我们希望过滤器不要拦截它们，以确保页面能够正确加载这些资源。
因此，可以在过滤器中对静态资源的请求路径进行排除或特殊处理，以允许这些请求继续通过，而不受过滤器的影响。
比如设置过滤器

```
if (req.getServletPath().endsWith(".png") || req.getServletPath().endsWith(".jpg")){
 chain.doFilter(req, res);}
}
因为浏览器加载 img 或者其他需要通过url获取资源的元素时，会向这个url发起请求，我们对 向项目下的.png,.jpg结尾的资源发起请求 的请求不进行拦截
```



# JSP

## 概述

1. JSP的全称是Java Server Pages，即Java的服务器页面
   JSP的主要作用是代替Servlet程序回传HTML页面的数据
   JSP页面本质上是一个Servlet程序，第一次访问JSP页面时(运行Tomcat服务器后在浏览器地址栏输入路径)，Tomcat服务器会将此JSP页面翻译成为一个Java源文件，并对其进行编译成为.class字节码文件.
   JSP翻译出来的Java类间接继承于HttpServlet类，证明JSP页面是一个Servlet程序
   而这个Servlet程序处理的请求地址就是jsp的地址
   JSP可以看作抽象的Servlet 运行时由服务器动态生成的，处理对JSP页面地址请求的Servlet
2. JSP是以 java语言为脚本语言，运行在服务器端的技术。
   必须由服务器端编译运行，客户端浏览器无法直接运行
   JSP隐式包含 req/resp/session等对象
3. jsp想要调试，需要启动服务器哦，因为浏览器无法直接运行
4. JSP文件可以像html一样写代码，直接编译成网页，多出的优势是可以写JSP代码
5. JSP中<%@ page contentType="text/html;charset=UTF-8" language="java" %>必须有
   声明jsp转为Servlet时使用的编码方式，如果没有 会乱码
6. 

## 语法

**<% %>**
JSP代码片段，java执行代码，在里面填上java代码

```jsp
<body>
<h1><%out.print("hello jsp")%></h1>
</body>//结果：h1标题大小的hello jsp
```

**<%=   %>**
JSP表达式，对象。而非执行代码
将里面的代码结果转化为字符串插入到表达式出现的地方

```jsp
<%for(int i=0;i<4;i++){%>
<%=i%>
<%}%>
```

**<%--注释--%>**

**<%@include file="地址"%>** 
直接引入文件，整合后编译。适合引入静态文件资源

被引入的文件的所有内容 会原封不动地插入到JSP代码的位置
这意味着在输出的最终 HTML 页面中，被引入文件的内容会替换 include 指令的位置，作为其中的一部分
但是这也可能造成一些问题：如果被引入的文件和当前 JSP 文件都包含 `<body>` 标签，这会导致 HTML 结构错误。在 HTML 中，每个页面应该只有一个 `<body>` 元素，多个 `<body>` 元素会导致解析问题。

## EL表达式

Expression Language
用EL表达式替代JSP标签，简化JSP页面的开发
支持直接访问request/session等隐式对象，也支持直接通过隐式对象获取其附加的属性对象
支持直接调用属性对象中封装的属性，也支持直接调用对象中的方法....

### 语法

**${  }**
声明EL表达式
${name} 依次从 page/request/session/application作用域中寻找指定名称的对象,没有则返回空字符串(不是null)

通过 对象.属性 获取对象的属性值
即使这个属性是private它也能获取，只要对象是按照规范定义的，那么就能获取
${user.userName} 其实是获取到user对象后隐式调用了 getuserName方法
如果不规范定义，没有定义这个方法，那么就获取不到这个值，所以说一定要规范

### 操作符

| 操作符     | 作用                       |
| ---------- | -------------------------- |
| .          | 访问属性或方法             |
| []         | 访问一个数组或者链表的元素 |
| ()         | 改变优先级                 |
| + - *      | 加减乘                     |
| / or div   | 除                         |
| % or mod   | 取模                       |
| == or eq   | 是否相等                   |
| != or ne   | 是否不等                   |
| < or it    | 是否小于                   |
| > or gt    | 是否大于                   |
| <= or le   | 是否小于等于               |
| >= or ge   | 是否大于等于               |
| && or and  | 逻辑与                     |
| \|\| or or | 逻辑或                     |
| ! or not   | 取反                       |
| empty      | 是否空                     |



### Limit

在对象名字前面加上这些限制，可以限制查找的范围/域

| 隐含对象         | 描述                          |
| ---------------- | ----------------------------- |
| pageScope        | page作用域                    |
| requestScope     | request作用域                 |
| sessionScope     | session作用域                 |
| applicationScope | application作用域             |
| param            | Request对象的参数，字符串     |
| paramValues      | Request对象的参数，字符串集合 |
| header           | HTTP信息头，字符串            |
| headerValues     | HTTP信息头，字符串集合        |
| initParam        | 上下文初始化参数              |
| cookie           | cookie的值                    |
| pageContext      | 当前页面的pageContext         |

获取对象时，不显式指定作用域，默认查找顺序：page/request/session/application，找到便停止查询返回对象

当有一个对象同时存在于 request 和 session中同名，但我们想要session中的它时
\${name}默认找完request后就返回了，找不到session中的对象
我们可以通过指定作用域来达到目的
\${sessionScope.name}就是在session中找name对象
(其实是先获取了session对象，然后调用这个对象中的name属性，效果上是在session作用域中找 name)

## JSPtags

JSTL提供了许多标签库，比如我们的 Core Tags

还有 Formatting tags,SQL tags,XML tags,JSTL Functions····
JSTL标签库有多个实现
怎么引入？
引入JSTL标准接口，引入JSTL标准实现

```
<!--JSTL接口依赖-->
        <!-- https://mvnrepository.com/artifact/jakarta.servlet.jsp.jstl/jakarta.servlet.jsp.jstl-api -->
        <dependency>
            <groupId>jakarta.servlet.jsp.jstl</groupId>
            <artifactId>jakarta.servlet.jsp.jstl-api</artifactId>
            <version>3.0.0</version>
        </dependency>
        <!--jstl实现依赖-->
        <!-- https://mvnrepository.com/artifact/org.glassfish.web/jakarta.servlet.jsp.jstl -->
        <dependency>
            <groupId>org.glassfish.web</groupId>
            <artifactId>jakarta.servlet.jsp.jstl</artifactId>
            <version>3.0.1</version>
        </dependency>
```

然后更新maven配置
依赖配置完后，通过 <%@ taglib prefix="c" uri="jakarta.tags.core" %>引入 core tags
如何使用标签？ <c:url var="base" value="/" /> 使用core tags里面的url标签
使用标签可以直接以 / 结尾 也可以 \<c:url> \</c:url> 这样包围

哪里能用到这个？项目部署
项目里有很多路径，部署路径，转发路径，重定向···
但是写静态路径的话，由于项目部署位置不确定，那肯定不行啊！所以我们需要动态获取项目的部署路径

使用 HTML里自带的\<base>标签，该标签的属性href代表当前页面下所有相对路径所相对的路径
\<base href="a"> 那么该页面下的所有相对路径都是相对 a 的路径
这个a也是静态的啊，如果这个a是项目的根路径就好了，所以我们只需要把这个href等于项目的根就行了
使用JSTL里的\<c:ulr> 标签

**\<c:url  var="" value="" >**
var=地址变量名称  value=地址
由于JSTL标签底层先转为java代码后在项目内运行，所以 value="/"这个/就代表项目的根路径
那么项目运行的时候，var地址变量所引用的地址就动态变成项目的根路径了！

综上

```
<c:url var="base" value="/" />用于动态获取项目根地址，用名为base的变量引用
<base href="${href}"> 利用EL表达式获取base对象，把这个路径作为当前页面的根
```

   



由于这些都是JSTL，所以都要运行在JSP类型的文件下面

### Core tags

 在页面使用标签库的前缀
\<%@ taglib prefix="c" uri="jakarta.tags.core" %>
tag library   prefix前缀

| 标签           | 描述                                          |
| -------------- | --------------------------------------------- |
| \<c:out>       | 用于显示数据类似<%= %>                        |
| \<c:set>       | 用于保存数据                                  |
| \<c:remove>    | 用于删除数据                                  |
| \<c:catch>     | 处理异常并且存储异常信息                      |
| \<c:if>        | 与 if 一样                                    |
| \<c:choose>    | 本身只当作\<c:when> \<c:ohterwise>的父标签    |
| \<c:when>      | \<c:choose>的子标签，用来判断条件是否成立     |
| \<c:ohterwise> | 同上，放在\<c:when>后，当条件不成立时执行这个 |
| \<c:import>    | 检索一个绝对或相对URL 将其内容暴露给页面      |
| \<c:forEach>   | 基础迭代标签，接收多种集合类型                |

 还有很多，但不能全说。
所有标签是 var属性代表变量名称，value 属性代表变量引用的对象
\<c:set var="name" value="value">
那么这个变量怎么获取？这个相当于设置了一个变量(var name=value)
用EL表达式获取 ${变量名}，便拿到了这个变量(对象)

#### \<c:set>

设置指定变量名称的值，默认在 page 级创建

```html
<c:set var="salary" value="1000" />
通过EL显示结果${salary}
```

 ![image-20240626155313723](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240626155313723.png)

#### \<c:if>

test属性  接收一个返回为boolean的表达式，如果 为 true则执行该标签的主体内容
1.主体内容应该放在\<c:if> 和 \</c:if> 之前，所以这个标签不能直接在内部用 / 结尾
2.表达式放在${} 里面,不然一律当html代码看，比如下面的\${salary>1000} 而不应该是 \${salary}>1000

```html
<c:if test="${salary>1000}" var="iftest">
    salary:${salary}大于1000
    ${iftest}
</c:if>
<c:if test="${salary <= 1000}">
    salary:${salary} 小于等于 1000
</c:if>
```

![image-20240626172749406](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240626172749406.png)





**\<c:choose>\<c:when>,\<c:otherwise>**
用于在众多选项中做出选择，与switch相同
\<c:when> switch中的case 选择的标准同样放在test属性里面
\<c:otherwise> switch中的default

```html
<c:choose>
    <c:when test="${salary>1000}">
        大于1000
    </c:when>
    <c:when test="${salary<1000}">
        小于1000
    </c:when>
    <c:otherwise>
        等于1000
    </c:otherwise>
</c:choose>
```

**\<c:forEach>**
迭代遍历元素，整合for/foreach等
Items 集合数组对象（必须通过EL表达式获得)
Var 每次迭代的元素对象
begin 开始的元素
end 最后的元素
step 每一步迭代的步长
varStatus 迭代状态变量

```html
@WebServlet("/hello")
public class testServ extends HttpServlet {
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) throws ServletException, IOException {
        User user1 =new User("1","1");
        User user2 =new User("2","2");
        User user3 =new User("3","3");
        List<User> users= List.of(user1,user2,user3);
        req.setAttribute("users",users);
        req.getRequestDispatcher("/Test/test.jsp").forward(req,resp);
    }
}
放入req对象中转发到jsp页面,jsp页面可以获取该对象然后遍历  必须用EL表达式获取对象哦!
<ul>
    <c:forEach items="${users}" var="u">
        <li>${u.userName}</li>
    </c:forEach>
</ul>
```

varStatus属性，封装遍历状态的属性遍历名称
index 当前迭代的索引，从0开始
count 当前迭代的次数，从1开始
frist 判断boolean 是否为第一项
last 判断 boolean 是否为最后一项

```html
<ul>
    <c:forEach items="${users}" var="u" varStatus="vs">
        <tr>
            <td>${u.userName}</td>
            <td>${vs.index}</td>
			<td>${vs.count}</td>
            <td>${vs.first}</td>
            <td>${vs.last}</td>
        </tr>
    </c:forEach>
</ul>
```

![image-20240626231439152](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240626231439152.png)





# JDBC

![image-20240626224251776](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240626224251776.png)

## 概述

JDBC是java提供（定义）的访问操作基于SQL标准数据库的规范
各数据库( *厂商* )实现JDBC规范，应用(app)改变数据库时，无需修改数据库源码，仅需更换JDBC
降低迁移/开发/维护的成本

其实就是java官方提供的一套规范(接口)。用于帮助开发人员快速实现不同关系型数据库的连接！

## 配置

**首先加入依赖并更新maven**

```html
    <dependencies>
        <!-- https://mvnrepository.com/artifact/jakarta.servlet/jakarta.servlet-api -->
        <dependency>
            <groupId>jakarta.servlet</groupId>
            <artifactId>jakarta.servlet-api</artifactId>
            <version>6.0.0</version>
            <scope>provided</scope>
        </dependency>
        <!-- https://mvnrepository.com/artifact/jakarta.servlet.jsp.jstl/jakarta.servlet.jsp.jstl-api -->
        <dependency>
            <groupId>jakarta.servlet.jsp.jstl</groupId>
            <artifactId>jakarta.servlet.jsp.jstl-api</artifactId>
            <version>3.0.0</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/org.glassfish.web/jakarta.servlet.jsp.jstl -->
        <dependency>
            <groupId>org.glassfish.web</groupId>
            <artifactId>jakarta.servlet.jsp.jstl</artifactId>
            <version>3.0.1</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
        <dependency>
            <groupId>com.mysql</groupId>
            <artifactId>mysql-connector-j</artifactId>
            <version>8.4.0</version>
        </dependency>
        <!-- https://mvnrepository.com/artifact/jakarta.annotation/jakarta.annotation-api -->
        <dependency>
            <groupId>jakarta.annotation</groupId>
            <artifactId>jakarta.annotation-api</artifactId>
            <version>2.1.1</version>
            <scope>provided</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.3.2</version>
            </plugin>
        </plugins>
    </build>
```

**配置DataSource**
在Webapp下创建META-INF目录，在该目录下创建文件，命名context.xml
在该文件里面添加Resource资源配置。(以上文件名称定死，不能随便起名)
容器启动应用时自动读取该配置文件，并按照配置自动创建数据源对象
我们按照里面创建的对象的名称（自定义）来获取对象

**context.xml**
里面放什么？里面的东西是什么？
项目声明的context.xml配置文件，Servlet容器启动时，根据此配置连接数据库，创建数据源对象
如果账号/密码/驱动类/URL地址等声明配置错误，将无法连接数据库，应用也无法启动

```
<?xml version="1.0" encoding="UTF-8" ?>
<Context>
    <Resource name="jdbc/MySQL" type="javax.sql.DataSource"
              maxTotal="100" maxIdle="30" maxWaitMillis="10000" initialSize="1"
              username="2022212891" password="123456"
              driverClassName="com.mysql.cj.jdbc.Driver" url="jdbc:mysql://116.63.13.220:3306/2022212891" />
</Context>
```

name  资源在JNDI树的名称（数据源对象的键）  这是我们自己命名的 jdbc/MySQL
type 是容器要创建的对象类型 我们在这儿创建一个 javax.sql.DataSource 类型的对象
url 连接到数据库的URL 这个是最重要的
![image-20240627201924618](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240627201924618.png)
diverClassName 驱动类  实现jdbc的入口

username/password 数据库访问用户名和密码
initialSize 初始化时池中默认创建的连接
maxTotal 最大并发连接数，0为无限制
maxWaitMillis 连接最大等待时间 超时则抛出异常
maxIdle 连接池中空闲连接最大数 -1无限制
Tomcat基于Apache DBCP2数据库连接池

容器(*Tomcat*)根据这些键值对创建对象，放到 JNDI树上 , 
*Tomcat*把这些对象的引用放在JNDI树上，我们在这个树上 去找数据源对象，拿过来之后直接调用
(数据源其实以键值对的形式保存，树上是他们的键，我们在树上通过键找到它们对应的值)



**连接数据库**
省略

**创建sql文件**
在resources下 new  选择 文件 ，**后缀写为sql**即可 如 ：*2022212891.sql*

## 使用

**DataSource**
java跟MySql创建连接进行互交
我们基于数据源创连接对象 Connection

数据源在项目启动时就要使用，所以我们用监听器监听项目启动，启动便创建数据源对象

```java
@WebListener
public class DataSourceUtils implements ServletContextListener {
    @Resource(name="jdbc/MySQL")
    private static DataSource dataSource;//Tomcat创建，直接注入进来给我们用 
    public static Connection getConnection() throws SQLException{
        return dataSource.getConnection();
    }//对外暴露获取连接的方法,这个方法有异常，谁用这个连接谁处理这个异常
}
```

### **Connection**

Interface java.sql.Connection java中的接口
叫做连接，应用/数据库数据互交的管道
在连接中执行SQL语句，返回SQL结果

通过  数据源对象.getConnection() 方法获得该类型的对象

在该连接对象下面获取执行者对象

### Statement

1. **Statement**

   普通执行者对象

   Statement接口，发送SQL语句至数据库，数据库编译语句，执行。无缓存

   方法
   **int executeUpdate(String sql)**
   将 sql 作为sql语句运行，返回影响的行数

   **ResultSet executeQuery(String sql)**
   将 sql作为SQL语句运行，返回ResultSet类型的对象，该对象内封装了查询的结果

   ```java
   String userName="pang";
   String password="123";
   Statement statement = connection.createStatement();
   statement.executeQuery("SELECT * FROM user WHERE"+"userName="+userName+"AND password="+password);
   ```

   这种执行对象的sql要手动拼接
   *"SELECT \* FROM user WHERE"+"userName="+userName+"AND password="+password*

2. **PreparedStatements**
   发送预编译SQL语句，数据库编译并缓存编译结果
   预编译语句可以复用，提高执行效率

   **int executeUpdate(String sql)**
   将 sql 作为sql语句运行，返回影响的行数

   **ResultSet executeQuery(String sql)**
   将 sql作为SQL语句运行，返回ResultSet类型的对象，该对象内封装了查询的结果

   这种方法无需拼接SQL语句，提高安全性

   sql语句中用 **？**作为占位符，位置从1计算

   获得完ps对象后，可以使用下面的方法在指定位置传递指定类型的参数
   ps.setXXX(index,XXX) 给ps对象中预编译的SQL语句的 ？占位符赋值
   setInt(int parameterIndex, int e)
   setString(int parameterIndex, String s)
   setDate(int parameterIndex, Date d)

   ```java
   String sql="UPDATE user SET name=? WHERE id=?"//预编译语句
   Connection conn= DataSource.getConnection()//这个是上面那个类的静态方法，获取连接对象 
   PreparedStatement ps=conn.prepareStatement(sql);//获得预编译对象后可以设置值了
   ps.setInt(2,2) 在第二个问号处传入int类型的值 2
   ps.setString(1,"peter") 在第一个问号处塞入字符串peter
   之后该对象内部预编译的sql语句就变成了  UPDATE user SET name="peter" WHERE id=2
   就可以执行sql语句了
   ps.executeQuery()
   ```

### ResultSet

封装查询结果集 对象

就是把整个表格装了进来刚开始游标在第一行前面

| id   | name  | Insert_time |
| ---- | ----- | ----------- |
| 1    | steve | xxx         |
| 2    | peter | xxx         |
| 3    | david | xxx         |

通过操作游标获取数据，游标移动到最后终止

1. Boolean next() 游标下移一行，移动到最后时返回false
2. Void beforeFirst() 游标返回第一行前面

取值操作
将当前行指定索引位置或者指定列名称的数据按照指定类型获取
XXX getXXX(int index)指定列按指定类型获取
XXX getXXX(String 字段)指定字段按指定类型获取

```
while(rs.next()){
rs.getInt("id") 以int类型获取这一行 字段为"id"列的值   ,
rs.getString("name") 以String 获取 这一行 字段为"name"的值
rs.getObject("insert_time",LocalDate.class) 获取这一列的值，但是 date 类型不能直接得，所以用 Object
}
```

所以即使数据列为整形，也可以按照String类型获取
但是数据类型转换失败会报抛出异常



**上述三种资源都需要关闭**
Connection,Statement,ResultSet
可以放在try()内自动关闭
也可以 对象.close() 手动关闭

## 原子性

数据库事务要保证 数据的一致性和原子性操作
但是JDBC默认自动提交，即executeUpdate()方法执行后就自动提交到数据库
现有这种情况
executeUpdate 后面还有一个 executeUpdate 但是两者中间抛了异常，导致后者没有执行，但是前者已经执行完毕传上去了
不符合数据库事务的原子性

修改连接属性为非自动提交！
connection对象.setAutoCommit(false)
直到所有操作完成后再改回来自动提交
connection对象.setAutoCommit(true)
保证操作的原子性，在没操作完成前，不提交到数据库上面

# MVC

项目的设计模式/思想
将软件分为三层
Model
业务逻辑层，存放数据

View
显示层，实现面向用户的数据显示，决定数据的显示方式，不关心数据怎么来，从哪儿来

Controller
控制层，向业务逻辑层发送请求数据，组织所需显示数据再发给显示层







- Step 1：controller接收用户请求，完成数据类型转换，数据校验，封装，调用model业务逻辑处理操作

- Step 2：model接收数据信息，基于具体业务逻辑完成业务操作，包括：完成对数据库的CRUD操作，将数据信息封装再返回给controller

- Step 3：controller继续调用其他model完成业务操作，最后组织view所需显示数据信息，将数据发送至view

- Step 4：view基于显示逻辑决定显示内容，基于显示模式，格式化数据信息并显示在页面

- Step 5：用户浏览显示内容，并基于显示内容完成下一轮请求数据的填充

- 无依赖，单向依赖

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629140444240.png" alt="image-20240629140444240" style="zoom:25%;" /> 



**反例**

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629140506826.png" alt="image-20240629140506826" style="zoom:50%;" /> 

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629140514479.png" alt="image-20240629140514479" style="zoom:50%;" /> 



<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629140522050.png" alt="image-20240629140522050" style="zoom:50%;" /> 

<img src="C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240629140531219.png" alt="image-20240629140531219" style="zoom:50%;" /> 

# MVVM模式

MVVM: Model View ViewModel
Model 数据部分
View 视图部分
ViewModel 用于连接视图与数据模型，负责监听View或者Model的改变



# 实践误区

1. String sql="select * from ? where tid=?";

   使用 preparement 预编译 sql语句时，表的名字不能动态设置！必须直接点名表的名字

2. 从页面链接 a href=xxx?tid=0 假设进入了 /home，/home 的Servlet类能从 req中拿到这个传进来的 tid
   然后这个tid在这个Servlet类中使用完毕后
   最后肯定会 req.getRequestDispatcher("/WEB-INF/pages/introductionTeachers.jsp").forward(req,resp); 
   是吧，那么我们在 introductionTeacher.jsp中可以使用 ${tid} 吗？
   不行！从链接传的 tid 在Servlet类中用完了，从servlet向jsp页面传的资源里面不存在这个tid, 想要使用就得手动在Servlet类中设置
   req.setAttribute("tid",tid)，记住了！ 

3. ![image-20240703204917193](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240703204917193.png)

   	奇怪为什么第二个 t.timg图片能正常加载出来？
   请问第一个t.timg t是哪来的？第一个t.timg使用时根本就没有t
   正确用法是用附近的 teacher
   ![image-20240703205018587](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240703205018587.png)

4. 不要想着 拦截 href="#" 的请求，这个代表超链接什么也不访问！
   ![image-20240703213848975](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240703213848975.png)
   看下面，请求的资源 /webc/  这里根本没有# 所以他就没有访问东西

5. req.getParameter()返回值是字符串
   req.getAttribute() 返回值是 Object 对象
   需要用的时候手动转换哦！



