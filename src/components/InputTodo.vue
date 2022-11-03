<script setup>
  import {ref} from 'vue'
  const textTask = ref("")
  const dateTask = ref("")

  const emit = defineEmits(['create'])

  const onAddTask = () =>{
    let  objTask  = {todo : textTask.value, date : dateTask.value}
    emit('create',objTask)
  }


</script>

<template>

  <h1>ToDo List</h1>
  <div class="todo__input">
    <form>
      <input type="text"
             v-bind:value = " textTask"
             @input = " textTask = $event.target.value"
      >
      <input type = "date" name = "date"
             id = "todo__input-date"
             :value = "dateTask"
             @input = "dateTask = $event.target.value"
      >
      <button @click.prevent = "onAddTask"
      >ADD </button>
      <p>{{textTask}} {{dateTask}}</p>
    </form>
  </div>

</template>


<style scoped>
  input{
    margin: 10px;
    border: none;
    border-bottom: solid 2px black;
    padding: 0.6em 1.2em;
    font-size: 1em;
    font-weight: 500;
    outline: none;
  }
</style>
