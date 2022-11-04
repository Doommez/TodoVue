<template>
  <div class="todo-creator">
    <textarea type="text"
              v-model="text"
    />
    <input type="date"
           name="date"
           id="todo__input-date"
           v-model="data"
    >
    <button @click="onAddTask">
      ADD
    </button>
    <div v-if="isValid"
       class="todo-creator__error"
    >
      enter value
    </div>
  </div>
</template>
<script setup>
  import {ref} from 'vue'

  const text = ref(null)
  const data = ref(null)
  const isValid = ref(false)

  const emit = defineEmits(['create'])

  const checkValid = () => {
    if (text.value === null) {
      isValid.value = true
      return true
    } else {
      isValid.value = false
      return false
    }
  }
  const onAddTask = () => {
    if (checkValid()) {
      return
    }
    let objTask = {todo: text.value, date: data.value, completed: false}
    emit('create', objTask)
    text.value = null;
    data.value = null;
  }
</script>

<style lang="scss" scoped>
  .todo-creator {
    display: flex;
    align-items: baseline;

    textarea {
      height: 20px;
      resize: none;
      margin: 10px;
      padding: 0px;
      border: none;
      border-bottom: solid 2px black;
      font-size: 1em;
      font-weight: 500;
      outline: none;
    }

    input {
      margin: 10px;
      border: none;
      border-bottom: solid 2px black;
      font-size: 1em;
      font-weight: 500;
      outline: none;
    }

    &__error {
      color: red;
      font-size: 20px;
    }
  }

</style>
