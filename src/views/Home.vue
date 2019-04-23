<template>
  <div id="app">
    <!-- now place AddTodo.vue -->
    <AddTodo v-on:add-todo="addTodo"/>
    <!-- get your component value here -->
    <!-- v-bind is use for data binding and we use here to bind the data of todos array -->
    <!-- now we use this binding data in our Todos.vue component using props -->
   <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />  
  </div>
</template>

<script>
//inport your vue file from components
import Todos from '../components/Todos';
import AddTodo from '../components/AddTodo';
import axios from 'axios';
export default {
  name: 'Home',
  //add compont here also
  components: {
    Todos,
    AddTodo
  },
  // data is a function that returns in object 
  data(){
    return {
      // todos is an array of object to print value to these array use {{todos}}
      todos: []
    }
  },
  methods: {
    deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err));
     // this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo){
      const {title, completed}= newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos' , {
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
      .catch(err => console.log(err));
      //spread operator to copy todos in newTodo
      //this.todos = [...this.todos, newTodo];
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => this.todos = res.data)
    .catch(err => console.log(err));
  }
}
</script>

<style>
*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}
.btn {
  display: inline-block;
  border: none;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}
.btn:hover {
  background: #666;
}
</style>
