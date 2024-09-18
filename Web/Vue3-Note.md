# 绑定

## 模板语法

又叫 **文本插值**

最基本的文本绑定形式是文本插值，使用的是  Mustache  语法 也就是**双大括号**！
**模板语法 {{  键  }}**
渲染出来是键对应的值，如果里面的键不存在对应的值，那么不渲染，也不会报错

App.vue里面改成这样

```vue
<template>
  <h3>123</h3>
  <p>{{ key }}</p>
  <p>{{ hello }}</p>
</template>

<script>
export default{
  data(){
    return{
      key:"key-object" ,
      hello: "hello world"
    }
  }
}
</script>

```

![image-20240728125414739](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240728125414739.png) 



在 JS 里面的键值对可以直接响应到页面里的模板语法中
JS里的多个键值对用逗号分隔

键值对的值可以是数字，字符串，也可以是布尔值  true  false
如果值本身包含双引号，需要用单引号代替



每个**{{}}**绑定仅支持**单一表达式**
如何判断表达式是否合法？这个表达式如果能放到return后面，那就是合法的。比如
return 1
return 1+2
return "123"+"45"
return ok?"yes":"no"
**只要是有返回值的表达式都可以**，但是只能放一个

```vue
<template>
  <h3>123</h3>
  <p>{{ number>number2?key:hello}}</p>
</template>

<script>
export default{
  data(){
    return{
      key:"key-object",
      hello:"hello world",
      number:10,
      number2:11
    }
  }
}
</script>
```

![image-20240728130047579](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240728130047579.png) 



由于是单一表达式，必须是单行的，你看 {{ if(ok){return 1} }}这个if语句，虽然也有返回值，但是换行了

建议不要在模板语法中做任何表达式操作，在JS中完成，直接把结果放在模板里

## 原始HTML

双大括号会把值作为纯文本插入，而不是HTML

```vue
<template>
  <p>{{ number>number2?key:hello}}</p>
  <P>{{ rawHtml }}</P>
</template>

<script>
export default{
  data(){
    return{
      rawHtml:"<a href='bilibili.com'>B站"
    }
  }
}
</script>
```

![image-20240728130819604](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240728130819604.png) 

可以看到，标签变成了文本，没有被识别，不能做出想象中的链接

如果想让他识别标签，将值作为HTML插入，需要在template的标签中使用   **v-html**  指令

```vue
 <p v-html="rawHtml"></p> 这样就会把rawHtml对应的值作为HTML插入到该P中
注意如果用了这个指令，这个P里面不能放东西如  <p v-html="rawHtml">123</p>   报错！
```



## 属性绑定

标签里有很多属性，这些属性也可以动态绑定  但是双大括号不能绑定HTML的attribute
想要绑定属性，需要使用 **v-bind** 指令，类似 v-html

假如我们定义了一个键值对 msg:"active"
我们想要这个值作为类名，那么能直接使 <div class="{{msg}}"\>吗？

```vue
<template>
 <div class="{{ msg }}">测试</div>
</template>

<script >
export default{
  data(){
    return{
      msg:"active"
    }
  }
}
</script>
```

![image-20240728132916275](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240728132916275.png) 

可以看到，双大括号并没有按照模板语法进行转换。就算把外面的双引号干掉也不行，直接就报错了

但是想让msg在class里面显示出它对应的active怎么做？  使用 v-bind

```vue
 <div v-bind:class="msg">测试</div>
v-bind:class="键"   直接把键扔进去
v-bind:class="{{键}}"  这样不对
```

![image-20240728132945923](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240728132945923.png) 



想用键值对动态设置标签的属性，需要在该属性前面加上v-bind:
标签里面的所有属性都可以使用这个动态绑定
如果现在想要设置一个id  就是 

```vue
 <div v-bind:id="id" v-bind:class="msg">测试</div>
```



如果绑定的值是null，那么该属性将会从元素上面移除，这个属性就没了

```vue
<template>
 <div v-bind:id="id" v-bind:class="msg">测试</div>
</template>
<script >
export default{
  data(){
    return{
      msg:null,  注意是null而不是字符串的"null"
      id:"tip"
    }
  }
}
</script>
```

![image-20240728133839433](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240728133839433.png)
文本绑定  双大括号 {{键}}
属性绑定 v-bind:属性="键"





由于 v-bind 非常常用，所以我们有了简写的方案：在属性前面直接加冒号，而不用写v-bind，即v-bind省略，一个冒号代表了v-bind:

```vue
<template>
 <div :id="id" :class="msg">测试</div>
 <button :disabled="disabled">button</button>
</template>

<script >
export default{
  data(){
    return{
      msg:null,
      disabled:false 注意这里不可以是"false"哦，键值对的值是只能是字符串的
      disabled: 0 也是同样的效果
    }
  }
}
</script>
```

![image-20240728134118073](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240728134118073.png) 



### 动态绑定多个值

```vue
<template>
 <div v-bind="object">测试</div>
</template>

<script >
export default{
  data(){
    return{
      object:{
        msg:"asd",
        disabled:0
      }
    }
  }
}
</script>
```

这样没问题，但是他会直接把值原样放入标签里，这些自定义的当然没用

![image-20240728134647063](C:/Users/13480/AppData/Roaming/Typora/typora-user-images/image-20240728134647063.png) 

所以想要真的一下子绑定多个值，要让键值对的键是具体的属性名称 

```vue
object:{
        class:"active",
        disabled:0
      }
```



# 渲染

## 条件渲染

v-if

v-else

v-else-if

v-show



- **v-if**
  用于条件性地渲染一块内容。这块内容只有在指令的表达式返回真时才会渲染

  ```vue
  <template>
   <div v-if="flag">这个指令是真的</div>
  </template>
  
  <script >
  export default{
    data(){
      return{
        flag:true
      }
    }
  }
  </script>
  ```

  v-if接受的指令是 flag ， 如果 flag的值是真的，那么这个标签就会被渲染

- **v-else**
  