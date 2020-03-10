<template>
  <div id="app">
    <Header/>
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from "./components/Todos"
import Header from './components/layouts/Header'
import AddTodo from './components/AddTodo'

export default {
  name: "App", // name of the component
  components: {
    // child components that this parent component has
    Todos, 
    Header, 
    AddTodo
  },
  data() {
    // data that this component has
    return {
      todos: [
        {
          id: 1,
          name: "todo one",
          completed: false
        },
        {
          id: 2,
          name: "todo two",
          completed: true
        },
        {
          id: 3,
          name: "todo three",
          completed: false
        }
      ]
    };
  }, 
  methods:{
    deleteTodo(id){
      this.todos = this.todos.filter( todo => todo.id !== id)
    }, 
    addTodo(newTodo){
      this.todos = [...this.todos, newTodo]
    }
  }
};
</script>

<style>
*,
*::before,
*::after {
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
