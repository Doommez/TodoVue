<script setup>
import {onMounted, ref} from "vue"
import InputTodo from './components/InputTodo.vue'
import TodoItem from './components/TodoItem.vue'
import TodoDone from "./components/TodoDone.vue"

  let todos = ref(
    [
      ]
  )
  const completeTodods = ref([]);

  onMounted( async () => {
    const array = await fetchTodos()
    array.sort((a,b) => {
      const dateObj = new Date();
      const month = dateObj.getUTCMonth() + 1;
      const day = dateObj.getUTCDate();
      const year = dateObj.getUTCFullYear();
      if (!a.date){
        a.date = `${day}.${month}.${year}`
      }if (!b.date) b.date = `${day}.${month}.${year}`
      return a.completed - b.completed
    } )
    console.log(array)
    todos.value=array

  })


  const fetchTodos = async () => {
    const response = await fetch('https://dummyjson.com/todos')
    let arrayTodos = await response.json()
    return   arrayTodos.todos
 }

  const createTodo = (todo) => {
    console.log(todo)
    console.log(completeTodods.value)
    const newarr = [...todos.value]
    const lastId = newarr.sort((a,b) => b.id - a.id)[0].id;
    const newTodo = {
      ...todo,
      id: lastId + 1
    }
    todos.value.push(newTodo)
    const newTodos = [...todos.value]
    newTodos.sort((a,b) => a.completed - b.completed)
    todos.value=newTodos
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
  <h1>ToDo List</h1>
  <div class="todo__input">
    <InputTodo  @create = "createTodo" />
  </div>
    <div class="container-header">
      <h2>Task</h2>
      <h2>Action</h2>
      <!--    <TodoDone :arrayDone = "completeTodods"/>-->
    </div>
    <ul class = "todolist">
      <TodoItem :todos = "todos" @done="doneTask" @remove = "deleteTask"/>
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
