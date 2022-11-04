<script setup>
import {ref, computed} from "vue";

const emit = defineEmits(['remove'])

defineProps({
  todos:Array
})

const currentTodo = ref({});
const allArrayTodo = ref([])

const completedTodo = computed( () => {
  currentTodo.value.completed=true
  allArrayTodo.value.sort((a,b) => a.completed - b.completed)
return  [...allArrayTodo.value,currentTodo.value]
})

const selectCurrentTodod = (todo,todos) => {
  currentTodo.value = todo
  allArrayTodo.value = todos
  completedTodo.value
}

</script>
<template>
  <li v-for = "todo in todos" :key="todo.id" :class="{'completed':todo.completed == true}" >
      <textarea type="text"
                :value="todo.todo"
                @input="todo.todo = $event.target.value"/>
    <p>{{todo.date}}</p>
    <button class="red" @click="selectCurrentTodod(todo,todos)">DONE</button>
    <button class="grey" @click="$emit('remove',todo)">DELETE</button>
  </li>
</template>

<style lang="scss" scoped>
  li{
    display: grid;
    grid-template-columns: 2fr 1fr 1fr 1fr;
    grid-template-rows: 1fr 1fr ;
    textarea{
      grid-row: 1/3;
      border:none;
      outline: none;
      resize: none;
      overflow: visible;
      font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
      font-size: 16px;
      line-height: 24px;
      font-weight: 400;
      min-height: 100px;
    }
    &.completed{
    position: relative;
      &:after{
      content: "";
      position: absolute;
      display: block;
      width: 100%;
      height: 5px;
      top: 20%;
      left: 0px;
      background: #1a1a1a;
     }
    }
    button{
      max-width: 200px;
      min-width: 105px;
      &.red {
        color: deeppink;
        border: solid 1px deeppink;
      }
      &.grey{
        border: solid 1px  silver;
      }
    }
  }
</style>
