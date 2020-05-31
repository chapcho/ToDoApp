<template>
  <div id="app">
    <todo-header></todo-header>
    <todo-input v-on:addTodo="addTodo"></todo-input>
    <todo-list v-bind:propsdata="todos" @removeTodo="removeTodo"></todo-list>
    <todo-footer v-on:removeAll="clearAll"></todo-footer>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader'
import TodoList from './components/TodoList'
import TodoInput from './components/TodoInput'
import TodoFooter from './components/TodoFooter'

var STORAGE_KEY = "chapcho-vue-todo";
var todoStorage = {
  fetch: function() {
    var todos = JSON.parse(localStorage.getItem(STORAGE_KEY) || "[]");
    todos.forEach(function(todo, index) {
      todo.id = index;
    });
    todoStorage.uid = todos.length;
    return todos;
  },
  save: function(todos) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todos));
  }
};

// visibility filters
// var filters = {
//   all: function(todos) {
//     return todos;
//   },
//   active: function(todos) {
//     return todos.filter(function(todo) {
//       return !todo.completed;
//     });
//   },
//   completed: function(todos) {
//     return todos.filter(function(todo) {
//       return todo.completed;
//     });
//   }
// };

export default {
  data() {
    return {
      todos: todoStorage.fetch()
    }
  },
  // watch todos change for localStorage persistence
  watch: {
    todos: {
      handler: function(todos) {
        todoStorage.save(todos);
      },
      deep: true
    }
  },
  methods: {
    addTodo(todoItem) {
      // 로컬 스토리지에 데이터를 추가하는 로직.
      this.todos.push({
        id: todoStorage.uid++,
        title: todoItem,
        completed: false,
        created: Date.now
      });
    },
    clearAll() {
      // localStorage.clear();
      this.todos = [];
    },
    removeTodo (todoItem) {
      this.todos.splice(this.todos.indexOf(todoItem),1);
      // localStorage.removeItem(todoItem);
    }    
  },
  created () {
    // if (localStorage.length > 0) {
    //   for (var i = 0; i < localStorage.length; i++) {
    //     this.todoItems.push(localStorage.key(i));
    //   }
    // }
  },  
  components: {
    TodoHeader,
    TodoList,
    TodoInput,
    TodoFooter
  }
}
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03)
  }
</style>
