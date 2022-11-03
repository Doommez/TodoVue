<script setup>
  import {onMounted, ref} from "vue";
  // This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import InputTodo from './components/InputTodo.vue'
import TodoList from './components/TodoList.vue'
import TodoDone from "./components/TodoDone.vue"

  let todos = ref([
        // {id: 1, todo: "do something 1", date: "20.01.22"},
        // {id: 2, todo: "do something 2", date: "20.01.22"},
        // {id: 3, todo: "do something 3", date: "20.01.22"},
        // {id: 4, todo: "do something 4", date: "20.01.22"}
      ]
  )

  const completeTodods = ref([]);

  onMounted( async () => {
  let array = await fetchTodos()
    array.length=5
    todos.value=array
    todos.value.forEach((item) => {
      if (!item.date){
        let dateObj = new Date();
        let month = dateObj.getUTCMonth() + 1;
        let day = dateObj.getUTCDate();
        let year = dateObj.getUTCFullYear();
        item.date = `${day}.${month}.${year}`
      }
    })
  })


  async function fetchTodos  (){
    const response = await fetch('https://dummyjson.com/todos')
    let arrayTodos = await response.json()
    return   arrayTodos.todos
 }

  function createTodo (todo){
    let lastId = todos.value[todos.value.length-1].id;
    lastId += 1;
    todo.id = lastId;
    todos.value.push(todo)
  }

  const deleteTask = (todo) =>{
      todos.value = todos.value.filter((item) =>{
        return item.id !== todo.id
      })
  }
  const doneTask = (todo) =>{
    completeTodods.value.push(todo)
    deleteTask(todo);
  }
</script>

<template>

  <InputTodo  @create = "createTodo" />
  <TodoList :array = "todos" @done="doneTask" @remove = "deleteTask"/>
  <TodoDone :arrayDone = "completeTodods"/>

</template>

<style scoped>



</style>
