

# Vue创建项目（webStom）

1.![](C:\Users\muxihong\Desktop\typoraProject\Vue\file\image-20221206153553663.png)

2.为创建选择相应的组件

![image-20230128165633261](C:\Users\muxihong\Desktop\typoraProject\Vue\file\image-20230128165633261.png)

选择自己需要的   按空格键是选择或者取消

![image-20230128165805162](C:\Users\muxihong\Desktop\typoraProject\Vue\file\image-20230128165805162.png)

项目结构

![image-20230128170216945](C:\Users\muxihong\Desktop\typoraProject\Vue\file\image-20230128170216945.png)









# 指令

## v-text

更新元素的文本内容。

```vue
<span v-text="msg"></span>
<!-- 等同于 -->
<span>{{msg}}</span>
```

## v-html

`v-html` 的内容直接作为普通 HTML 插入—— Vue 模板语法是不会被解析的。如果你发现自己正打算用 `v-html` 来编写模板，不如重新想想怎么使用组件来代替。

```vue
<div v-html="html"></div>
```

## v-show

基于表达式值的真假性，来改变元素的可见性。       v-show一开始是吧标签渲染出来的，只不过是没有显示而已     和v-if有区别的一点是v-if 控制元素是否渲染到页面

`v-show` 通过设置内联样式的 `display` CSS 属性来工作，当元素可见时将使用初始 `display` 值。当条件改变时，也会触发过渡效果。

```vue
<template>
  <div>
<!--    <div v-if="num>90">显示</div>-->
    <div v-show="flag">显示</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      flag:false
    }
  },
  methods: {

  }
}
</script>
```

## v-once

仅渲染元素和组件一次，并跳过之后的更新。

```vue
<!-- 单个元素 -->
<span v-once>This will never change: {{msg}}</span>
<!-- 带有子元素的元素 -->
<div v-once>
  <h1>comment</h1>
  <p>{{msg}}</p>
</div>
<!-- 组件 -->
<MyComponent v-once :comment="msg" />
<!-- `v-for` 指令 -->
<ul>
  <li v-for="i in list" v-once>{{i}}</li>
</ul>

```

## v-if

基于表达式值的真假性，来条件性地渲染元素或者模板片段。**当同时使用时，`v-if` 比 `v-for` 优先级更高。**

当 `v-if` 元素被触发，元素及其所包含的指令/组件都会销毁和重构。如果初始条件是假，那么其内部的内容根本都不会被渲染。

```vue
<template>
  <div>
    <div v-if="num>90">显示</div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      num:80
    }
  },
  methods: {
  }
}
</script>
```

## v-for

基于原始数据多次渲染元素或模板块。

```vue
<div v-for="item in items">
  {{ item.text }}
</div>
```

或者，你也可以为索引指定别名 (如果用在对象，则是键值)：

```vue
<div v-for="(item, index) in items"></div>
<div v-for="(value, key) in object"></div>
<div v-for="(value, name, index) in object"></div>
```

`v-for` 的默认方式是尝试就地更新元素而不移动它们。要强制其重新排序元素，你需要用特殊 attribute `key` 来提供一个排序提示：

```vue
<div v-for="item in items" :key="item.id">
  {{ item.text }}
</div>
```

## v-on

给元素绑定事件监听器。   **期望的绑定值类型：**`Function | Inline Statement | Object (不带参数)`   最好是和方法绑定

```vue
<template>
  <div>
    <span>值为：{{num}}</span>
    <button v-on:click="addOne(num)">点击</button>
  </div>
</template>
<script>
export default {
  data(){
    return{
      num:0
    }
  },
  methods:{
    addOne(num){
      this.num+=1;
    }
  }
}
</script>
```

如果事件绑定函数调用，那么事件对象必须作为最后一个参数显示传递，并且事件对象的名称必须是$event

```vue
<template>
  <div>
    <span>值为：{{num}}</span>
    <button v-on:click="addOne(num,$event)">{{num}}</button>
  </div>
</template>
<script>
export default {
  data(){
    return{
      num:0
    }
  },
  methods:{
    addOne(num,event){
      this.num+=1;
      console.log(event.target.innerHTML)
    }
  }
}
</script>
```

## v-model

在表单输入元素或组件上创建双向绑定。    **期望的绑定值类型**：根据表单输入元素或组件输出的值而变化

```vue
<template>
  <div>
    <h1>{{msg}}</h1>
    <input type="text" v-model="msg">
  </div>
</template>
<script>
export default {
  data(){
    return{
      msg:""
    }
  }
}
</script>
```

## v-bind

属性绑定

```vue
<template>
  <div>
    <div><a :href="url">baidu</a></div>
    <button v-on:click="changeUrl">切换</button>
  </div>
</template>
<script>
export default {
  data(){
    return{
      num:0,
      url:'www.baidu.com'
    }
  },
  methods:{
    changeUrl(){
      this.url='www.bilibili.com';
    }
  }
}
</script>
```

样式绑定

```vue
<template>
  <div>
<!--    <div v-bind:class="{active:isActive}"></div>-->
<!--    <div v-bind:class="{active:isActive,error:errorClass}"></div>-->
<!--  第二种方式  -->
    <div v-bind:class="[isActive]"></div>
<!--  样式对象  -->
    <div v-bind:style="testStyle1"></div>
<!--  样式值  -->
    <div v-bind:style="{width:width,height: '200px',border: '1px solid pink'}"></div>
<!--  数组形式  -->
    <div v-bind:style="[testStyle1,testStyle2]"></div>
    <br>
    <button v-on:click="isActiveFunction">切换</button>
  </div>
</template>
<script>
export default {
  data() {
    return {
      num: 0,
      url: 'www.baidu.com',
      isActive: 'active',
      width:'100px',
      testStyle1:{
        width:"200px",
        height:"100px",
        border:"1px solid blue"
      },
      testStyle2:{
        background:'red'
      }
    }
  },
  methods: {
    changeUrl() {
      this.url = 'www.bilibili.com';
    },
    isActiveFunction() {
      this.isActive='active1'
    }
  }
}
</script>

<style scoped>
.active {
  width: 100px;
  height: 100px;
  border: 1px solid red;
}
.active1 {
  width: 200px;
  height: 200px;
  border: 1px solid green;
}
</style>
```

## 自定义指令

# 常用特性

## 表单处理

## 计算属性

computed中的计算属性依赖于data()中的数据，如果data()中的数据发生变化，那么计算属性中的数据则回重新计算

```vue
<template>
  <div>
    <p>Has published books:</p>
    <span>{{publishedBooksMessage}}</span>
    <span>{{now}}</span>
    <br>
    <span>{{fullName.get}}</span>
  </div>
</template>
<script>
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      },
      firstName:"",
      lastName:""
    }
  },
  methods: {
  },
  //计算属性
  computed:{
    publishedBooksMessage(){
      return this.author.books.length > 0 ? 'Yes' : 'No'
    },
    now() {
      return Date.now()
    },
    fullName:{
      get(){
        return this.author.name;
      },
      set(name){
        [this.firstName,this.lastName] = this.author.name.split(" ")
      }
    }
  }

}
</script>
```

## 监听器

应用场景：数据变化时执行异步或开销比较大的操作

```vue
<template>
  <div>
    <div>
      <span>名：</span>
      <span>
        <input type="text" v-model="firstName">
      </span>
    </div>
    <div>
      <span>姓：</span>
      <span>
        <input type="text" v-model="lastName">
      </span>
    </div>
    <div>{{fullName}}</div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      firstName:"joe",
      lastName:"Bob",
      fullName: 'joe Bob'
    }
  },
  watch:{
    firstName:function (val){
      this.fullName = val+' '+this.lastName;
    },
    lastName:function (val){
      this.fullName = this.firstName+' '+val
    }
  }
}
</script>
```

应用场景-判断用户名是否被注册过

```vue
<template>
  <div>
    <div>
      <span>用户名：</span>
      <span>
        <input type="text" v-model.lazy="name">
      </span>
      <span>{{msg}}</span>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      name:"",
      msg:''
    }
  },
  methods:{
    checkName(name){
      var that = this;
      setTimeout(function (){
        if (name==='admin'){
          that.msg='用户名已存在'
        }else {
          that.msg='用户名可以使用'
        }
      },2000)
      //接口调用
    }
  },
  watch:{
    name:function (val){
      //调用接口验证用户名合法性
      this.checkName(val);
      this.msg="正在验证...."
    }
  }
}
</script>
```

## 过滤器 

![image-20230128145450967](C:\Users\muxihong\Desktop\typoraProject\Vue\file\image-20230128145450967.png)

## 组件

### 组件注册
