<template>
  <div id="app">
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos 
      v-bind:todos="todos" 
      v-on:del-todo="deleteTodo" 
      v-on:update-todo="updateTodo" />
  </div>
</template>

<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";

export default {
  name: "Home",
  components: {
    Todos,
    AddTodo,
  },
  data() {
    return {
      todos: [],
    };
  },
  methods: {
    updateTodo(id) {
      this.todos[this.todos.findIndex(todo => todo.id === id)].completed = !this.todos[this.todos.findIndex(todo => todo.id === id)].completed
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    addTodo(newTodo) {
      this.todos = [... this.todos, newTodo];
    }
  },
  created() {
    fetch('https://jsonplaceholder.typicode.com/todos')
      .then(response => response.json())
      .then(json => this.todos=json)
  }
};
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }

  .btn {
    display: inline-block;
    border: none;
    background: #555;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
  }

  .btn:hover {
    background: #666;
  }
</style>
