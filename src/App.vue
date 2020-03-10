<template>
  <div id="app">
    <Header/>
    <!-- when we listen to the occurence of the custom event of add-todo, we invoke addTodo -->
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from "./components/Todos"
import Header from './components/layouts/Header'
import AddTodo from './components/AddTodo'
import axios from 'axios'

export default {
  name: "App", // name of the component
  components: {// child components that this parent component has
    Todos, 
    Header, 
    AddTodo
  },
  data() {
    // data that this component has
    return {
      todos: []
    };
  }, 
  methods:{
    deleteTodo(id){
      axios
      .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then( res => {
        console.log(res)
        this.todos = this.todos.filter(todo=> todo.id !== id)
      })
      .catch(err => console.log(err))
    }, 
    addTodo(newTodo){
      const {title, completed} = newTodo
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
        title, 
        completed
      }).then(res => this.todos = [...this.todos, res.data])
        .catch(error => console.log(error))
    }
  }, 
  created(){//similar to react/componentDidMount
    axios
    .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
    .then(res => this.todos = res.data)
    .catch(error => console.log(error))
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
