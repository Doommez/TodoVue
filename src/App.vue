<template>
  <div class="todo">
    <div class="todo-title">
      Todo list
    </div>
    <todo-create @create="createTodo"/>
    <div class="todo-list grid">
      <div class="grid__row grid__row__head">
        <div>
          Task
        </div>
        <div></div>
        <div>
          Action
        </div>
      </div>
      <div
        v-if="sortedTodosArray.length <= 0"
        class="todo-list__loading"
      >
        LOADING...
      </div>
      <todo-item
        v-for="todo in sortedTodosArray"
        :key="todo.id"
        class="todo-list__item grid__row"
        :todo="todo"
        :class="{'completed': todo.completed}"
        @remove="deleteTask"/>
    </div>
  </div>
</template>

<script setup>
  import {onMounted, ref, computed} from "vue";
  import TodoCreate from "./components/TodoCreate.vue";
  import TodoItem from "./components/TodoItem.vue";

  const todos = ref([])

  const fetchTodos = async () => {
    return (await fetch('https://dummyjson.com/todos')).json()
  }

  const mappingDateFetchTodos = (todosArray) => {
    const dateObj = new Date();
    const month = dateObj.getUTCMonth() + 1;
    const day = dateObj.getUTCDate();
    const year = dateObj.getUTCFullYear();
    todosArray.forEach(todo => {
      if (!todo.date) {
        todo.date = `${year}-${month}-${day > 10 ? day : "0" + day}`
      }
    })
  }

  const sortedTodosArray = computed(() => {
    if (todos.value.length !== 0) {
      const newSortTodoList = [...todos.value];
      return newSortTodoList.sort((firstTodo, secondTodo) => {
        if (firstTodo.completed < secondTodo.completed) {
          return -1
        }
        if (firstTodo.completed > secondTodo.completed) {
          return 1
        }
        return 0
      })
    }
    return todos.value
  })

  onMounted(async () => {
    todos.value = (await fetchTodos()).todos;
    mappingDateFetchTodos(todos.value)
  })

  const getMaxId = () => {
    const idexesArray = [];
    todos.value.forEach(todo => {
      idexesArray.push(todo.id)
    })
    return Math.max(...idexesArray)
  }

  const createTodo = (todo) => {
    const newTodo = {
      ...todo,
      id: getMaxId() + 1
    }
    todos.value.unshift(newTodo)
  }

  const deleteTask = (id) => {
    const indexTodo = todos.value.findIndex(todo => todo.id === id)
    todos.value.splice(indexTodo, 1)
  }

</script>

<style lang="scss" scoped>
  .todo-title {
    font-size: 38px;
    font-weight: bold;
  }

  .todo-list {
    margin-top: 15px;
  }

  .grid {
    display: grid;

    &__row {
      display: grid;
      grid-template-columns: 1fr 1fr 1fr;
      grid-template-rows: 1fr;
      align-items: center;
      justify-items: center;
      gap: 30px;

      &__head {
        font-size: 28px;
        font-weight: bold;
        margin-bottom: 10px;
      }
    }
  }
</style>
