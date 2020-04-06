<template>
  <div id="app">
    <ToHeader />
    <ToInput v-on:addTodo="addTodo" />
    <ToList v-bind:propsdata="todoItems" @removeTodo="removeTodo" />
    <ToFooter @removeAll="clearAll" />
  </div>
</template>

<script>
  // import HelloWorld from './components/HelloWorld.vue';
  // import Header from './components/Header';
  // import Menu from './components/Menu';
  // import Content from '@/components/Content';

  //자기 관리 프로그램 컴포넌트
  import ToHeader from './components/TodoIt/ToHeader';
  import ToFooter from './components/TodoIt/ToFooter';
  import ToInput from './components/TodoIt/ToInput';
  import ToList from './components/TodoIt/ToList';

  export default {
    name: 'App',
    components: {
      ToHeader,
      ToFooter,
      ToInput,
      ToList
    },
    data() {
      return {
        todoItems: []
      };
    },
    created() {
      if (sessionStorage.length > 0) {
        for (var i = 0; i < sessionStorage.length; i++) {
          this.todoItems.push(sessionStorage.key(i));
        }
      }
    },
    methods: {
      addTodo(todoItem) {
        sessionStorage.setItem(todoItem, todoItem);
        this.todoItems.push(todoItem);
      },
      clearAll() {
        sessionStorage.clear();
        this.todoItems = [];
      },
      removeTodo(todoItem, index) {
        sessionStorage.removeItem(todoItem);
        this.todoItems.splice(index, 1);
      }
    }
  };
</script>

<style>
  /* #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  } */
  body {
    text-align: center;
    background-color: #f6f6f8;
  }
  input {
    border-block-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgb(0, 0, 0, 0.03);
  }
</style>
