---
title: "Vue组件之间的传值"
date: 2019-05-11
permalink: "/frame/Vue组件之间的传值"
meta:
  - name: description
    content: 一个热爱文学的伪程序猿，张努力，Node，webpack，JavaScript，爱好者，博客
  - name: keywords
    content: 一个热爱文学的伪程序猿，张努力，Node，webpack，JavaScript，爱好者，博客
---
# Vue组件之间的传值

## 父组件向子组件传值

- `props`传值

  - 可以传递字符串，数组，对象...

- 子组件写法

  ```vue
  <template>
    <span>{{ title }}</span>
  </template>
  <script>
  export default {
    props: ['title']
  };
  </script>
  
  
  ```

  - 子组件通过`props`来接收父组件传递过来的值

  - 上面的`props`是数组的写法，也可以写成对象的方式，可以规定父组件传递过来的值是什么类型

    ```vue
    <template>
      <span>{{ title }}</span>
    </template>
    <script>
    export default {
      props: {
        title: String
      }
    };
    </script>
    ```

    

- 父组件写法

  ```vue
  <template>
    <div>
      <Children title='测试'></Children>
    </div>
  </template>
  <script>
  import Children from "./components/children";
  export default {
     components: {
      Children
    },
  };
  </script>
  ```

  - 还可以动态的传值，通过`v-bind`传递动态数据

    ```vue
    <template>
      <div>
        <Children v-bind:title="test"></Children>
      </div>
    </template>
    <script>
    import Children from "./components/children";
    export default {
      data() {
        return {
          test: "测试"
        };
      },
      components: {
        Children
      }
    };
    </script>
    ```

    

##  子组件向父组件传递数据

- 子组件主要通过事件给父组件传递消息

- 通过使用`$emit`发射事件

- 子组件写法

  ```vue
  <template>
    <div>
      <button @click="handEmit"></button>
    </div>
  </template>
  <script>
  export default {
    data() {
      return {
        list: [1, 2]
      };
    },
    methods: {
      handEmit() {
        this.$$emit("pops", this.list);
      }
    }
  };
  </script>
  
  ```

  

- 父组件写法

  ```vue
  <template>
    <div>
      <Children @pops="getData"></Children>
    </div>
  </template>
  <script>
  import Children from "./components/children";
  export default {
    data() {
      return {
        list: null
      };
    },
    methods: {
        //处理子组件的数据
      getData(data) {
        this.list = data;
      }
    },
    components: {
      Children
    }
  };
  </script>
  ```

  

- 子组件之间相互传递
  - 子组件与子组件没有直接的传递方法
  - 可以先传递给父组件，再通过父组件传递给字组件