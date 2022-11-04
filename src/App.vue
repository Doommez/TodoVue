<script setup>
import {onMounted, ref} from "vue"
import TodoItem from './components/TodoItem.vue'
import TodoCreate from "./components/TodoCreate.vue";

  let todos = ref(
    [
      ]
  )

const fetchTodos = async () => {
  const response = await fetch('https://dummyjson.com/todos')
  let arrayTodos = await response.json()
  return   arrayTodos.todos
}

onMounted( async () => {
  const array = await fetchTodos()
  const dateObj = new Date();
  const month = dateObj.getUTCMonth() + 1;
  const day = dateObj.getUTCDate();
  const year = dateObj.getUTCFullYear();
  array.sort((a,b) => {
    if (!a.date){
      a.date = `${day}.${month}.${year}`
    }if (!b.date) b.date = `${day}.${month}.${year}`
    return a.completed - b.completed
  } )
  todos.value=array
})

const createTodo = (todo) => {
  const newarr = [...todos.value]
  const lastId = newarr.sort((a,b) => b.id - a.id)[0].id;
  const newTodo = {
    ...todo,
    id: lastId + 1
  }
  todos.value.unshift(newTodo)
  const newTodos = [...todos.value]
  newTodos.sort((a,b) => a.completed - b.completed)
  todos.value=newTodos
}

const deleteTask = (todo) =>{
    todos.value = todos.value.filter((item) =>{
      return item.id !== todo.id
    })
}

</script>

<template>
  <h1>ToDo List</h1>
  <div class="todo__input">
    <TodoCreate  @create = "createTodo" />
  </div>
    <div class="container-header">
      <h2>Task</h2>
      <h2>Action</h2>
    </div>
    <ul class = "todolist">
      <TodoItem :todos = "todos" @remove = "deleteTask"/>
    </ul>


</template>

<style lang="scss" scoped>
.container-header {
  display: flex;
  justify-content: space-around;
}
ul{
    list-style-type: none;
    padding: 0px;
    margin: 0px;
}
</style>
