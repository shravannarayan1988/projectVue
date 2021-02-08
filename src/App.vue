<template>
  <div id="app">
  <Header></Header>
  <AddToDo v-on:add-todo="addTodo"></AddToDo>
  <Todos v-bind:todos="todos" v-on:del-todo="deletetodo" />
  </div>
</template>

<script>
import Header from './components/Header'
import Todos from './components/Todos'
import AddToDo from './components/AddToDo'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    Todos,
    Header,
    AddToDo
  },
  data(){
    return{
      todos:[]
    }
  },
  methods:{
    deletetodo(id){
      this.todos=this.todos.filter(todo=>todo.id!==id)
    },
     addTodo(newTodo){
       const{title,completed}=newTodo;
       axios.post('https://jsonplaceholder.typicode.com/todos',{
         title,
         completed
       })
       .then(res=>this.todos=[...this.todos,res.data])
       .catch(err=>console.log(err));
    
  }
  },
  created(){
    axios.get('https://jsonplaceholder.typicode.com/todos')
    .then(res=>this.todos=res.data)
    .catch(error=>console.log(error))
  }
 
}
</script>

<style>

</style>
