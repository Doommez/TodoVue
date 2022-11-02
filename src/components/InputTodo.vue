<script setup>
  import { ref } from 'vue'
  const textTask = ref({value:""})
  const dateTask = ref({value:""})

</script>

<template>
  <h1>ToDo List</h1>
  <div class="todo__input">
    <form>
      <input type="text"
             v-bind:value="textTask.value"
             @input="textTask.value = $event.target.value"
      >
      <input type="date" name="date"
             id="todo__input-date"
             :value="dateTask.value"
             @input="dateTask.value = $event.target.value"
      >
      <button @click.prevent="addTask"
      >ADD </button>
      <p>{{textTask.value}} {{dateTask.value}}</p>
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
