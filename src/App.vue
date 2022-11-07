<template>
  <div class="todo-title">Todo list</div>
  <TodoCreate @create="createTodo"/>
  <div class="todo-list">
    <div class="todo-list__title">Task</div>
    <div class="todo-list__title">Action</div>
    <div
      class="todo-list__loading"
      v-if="!sortTodosArray"
    >
      LOADING...
    </div>
    <TodoItem class="todo-list__item"
              v-for="item in sortTodosArray"
              :key="item.id"
              :class="{'completed': item.completed}"
              :item="item"
              @changeCompleted="changeCurrentTodoCompleted"
              @remove="deleteTask"/>
  </div>
</template>

<script setup>
  import {onMounted, ref, computed} from "vue"
  import TodoCreate from "./components/TodoCreate.vue";
  import TodoItem from "./components/TodoItem.vue";

  let todos = ref(null)

  const fetchTodos = async () => {
    const response = await fetch('https://dummyjson.com/todos')
    const arrayTodos = await response.json()
    return arrayTodos.todos
  }

  const sortTodosArray = computed(() => {
    if (!todos.value) {
      return todos.value
    }
    const newSortTodoList = [...todos.value];
    const dateObj = new Date();
    const month = dateObj.getUTCMonth() + 1;
    const day = dateObj.getUTCDate();
    const year = dateObj.getUTCFullYear();
    return newSortTodoList.sort((a, b) => {
      if (!a.date) {
        a.date = `${year}-${month}-${day > 10 ? day : "0" + day}`
      }
      if (!b.date) {
        b.date = `${year}-${month}-${day > 10 ? day : "0" + day}`
      }
      return a.completed - b.completed
    })
  })

  onMounted(() => {
    fetchTodos()
      .then(result => todos.value = result)
  })

  const getMaxId = () => {
    const lastId = todos.value.sort((a, b) => b.id - a.id)[0].id;
    return lastId
  }

  const createTodo = (todo) => {
    const newTodo = {
      ...todo,
      id: getMaxId() + 1
    }
    todos.value.unshift(newTodo)
  }

  const changeCurrentTodoCompleted = (todo) => {
    todo.completed = true
  }

  const deleteTask = (todo) => {
    let positionDelTodo = todos.value.indexOf(todo);
    if (positionDelTodo >= 0) {
      todos.value.splice(positionDelTodo, 1)
    }
  }

</script>


<style lang="scss" scoped>
  .todo-title {
    font-size: 38px;
    font-weight: bold;
  }

  .todo-list {
    display: grid;
    grid-template-columns: 2fr 2fr;
    grid-gap: 10px;
    grid-auto-rows: minmax(100px, auto);
    align-items: center;

    &__title {
      font-size: 28px;
      font-weight: bold;
    }

    &__loading {
      font-weight: bold;
      grid-column: 1/2;
    }

    &__item {
      grid-column: 1/3;
      display: flex;
      justify-content: space-between;
      align-items: baseline;
    }
  }
</style>
