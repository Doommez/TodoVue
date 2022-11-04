<script setup>
  import {ref} from 'vue'
  const textTask = ref("")
  const dateTask = ref("")
  const isValid = ref(false)

  const emit = defineEmits(['create'])

  const onAddTask = () =>{
    if (!!textTask.value == ""|| !!dateTask.value === ""){
     isValid.value = !isValid.value
      return
    }else isValid.value = false
    let  objTask  = {todo : textTask.value, date : dateTask.value, completed: false}
    emit('create',objTask)
  }


</script>

<template>


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
    </form>
    <p v-if="isValid"
       class="errorValid">enter value</p>


</template>


<style scoped>
  input {
    margin: 10px;
    border: none;
    border-bottom: solid 2px black;
    padding: 0.6em 1.2em;
    font-size: 1em;
    font-weight: 500;
    outline: none;
    height: 40px;
  }
  .errorValid{
    color: red;
    font-size: 30px;
  }
</style>
