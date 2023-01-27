# Vue

## Vue创建项目（webStom）

1.![](C:\Users\muxihong\Desktop\typoraProject\Vue\file\image-20221206153553663.png)

2.为创建选择相应的组件

## 指令

### v-text

更新元素的文本内容。

```vue
<span v-text="msg"></span>
<!-- 等同于 -->
<span>{{msg}}</span>
```

### v-html

`v-html` 的内容直接作为普通 HTML 插入—— Vue 模板语法是不会被解析的。如果你发现自己正打算用 `v-html` 来编写模板，不如重新想想怎么使用组件来代替。

```vue
<div v-html="html"></div>
```

### v-show

基于表达式值的真假性，来改变元素的可见性。

`v-show` 通过设置内联样式的 `display` CSS 属性来工作，当元素可见时将使用初始 `display` 值。当条件改变时，也会触发过渡效果。

### v-if

基于表达式值的真假性，来条件性地渲染元素或者模板片段。**当同时使用时，`v-if` 比 `v-for` 优先级更高。**

当 `v-if` 元素被触发，元素及其所包含的指令/组件都会销毁和重构。如果初始条件是假，那么其内部的内容根本都不会被渲染。

### v-for

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

### v-on

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



### v-model

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

### v-once

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

