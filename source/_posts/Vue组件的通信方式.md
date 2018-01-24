---
title: Vue组件的通信方式
date: 2018-1-3 17:46:00
tags: Vue
---


> 组件实例的作用域是**孤立的**，父组件的数据需要通过 **prop** 才能下发到子组件中
>
> Prop 是单向绑定的：当父组件的属性变化时，将传导给子组件，但是反过来不会。这是为了防止子组件无意间修改了父组件的状态。



#### 父传子

假设有message的字符串要从父组件传向子组件

Father.vue

```vue
<template>
	<div>
      <!--通过v-bind向子组件传递数据-->
      <child :message=message></child> 
  	</div>
</template>

<script>
  export default {
    name: 'father',
    components: {
      child
    },
    data() {
      return {
        message: 'Hello'
      }
    }
  }
</script>
```



Child.vue

```vue
<script>
  export default {
    name: 'child',
    props: {    //子组件要通过props声明预期的参数
      message: {
        type: String  //如果可以，尽量声明子组件预期的数据类型
      }
    },
    mounted() {
      console.log(message)  //Hello
    }
  }
</script>
```





#### 子传父

假设子组件要传递字符串note给父组件

Child.vue

```vue
<script>
  export default {
    name: 'child',
    data() {
      return {
        note: "hello"
      }
    },
    mounted() {
      this.$emit('postNote',this.note) //第二个参数为要传递的数据
    }
  }
</script>
```



Father.vue

```vue
<template>
	<div>
      <!--父组件通过v-on监听子组件emit出来的事件，并响应-->
      <child v-on:postNote="setNote"></child> 
  	</div>
</template>

<script>
  export default {
    name: 'father',
    components: {
      child
    },
    methods: {
      setNote(note) {
        console.log(note) //hello
      }
    }
  }
</script>
```





#### 兄弟组件间

兄弟组件间通信需要用到eventBus

假设有字符串hello world要从emit组件传递到on组件

首先，新建一个eventBus.js （假设新建在../assets文件夹中）

```javascript
import Vue from 'vue'
export default new Vue()
```



然后，数据发送和接收方都引入eventBus

数据传出方 emit.vue

```vue
<script>
  import bus from '../assets/eventBus.js'
  export default {
    name: 'emit',
    mounted() {
      bus.$emit("start","hello world") //通过bus携带数据用start事件$emit出来
    }
  }
</script>
```



数据接收方 on.vue

```vue
<script>
  import bus from '../assets/eventBus.js'
  export default {
    name: 'on',
    mounted() {
      bus.$on("start",function(text) { //通过bus，用$on监听
        console.log(text) //hello world
      })
    }
  }
</script>
```





