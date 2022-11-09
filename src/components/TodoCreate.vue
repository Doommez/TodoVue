<template>
  <div class="todo-creator">
    <textarea
      v-model="valueTextarea"
    />
    <input
      v-model="valueDataInput"
      name="date"
      type="date"
    >
    <button
      class="todo-creator__button"
      :disabled="!isInValid"
      @click="onAddTask"
    >
      ADD
    </button>
  </div>
</template>
<script setup>
  import {ref, computed} from 'vue'

  const valueTextarea = ref(null)
  const valueDataInput = ref(null)

  const emit = defineEmits([
    'create',
  ])

  const isInValid = computed(() => valueTextarea.value && valueDataInput.value);

  const onAddTask = () => {
    if (isInValid) {
      const objTask = {
        todo: valueTextarea.value,
        date: valueDataInput.value,
        completed: false
      }
      emit('create', objTask)
      valueTextarea.value = null;
      valueDataInput.value = null;
    }
  }
</script>

<style lang="scss" scoped>
  .todo-creator {
    display: grid;
    grid-template-columns:1fr 40% 20%;
    align-items: center;

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

    button {
      align-self: center;
      justify-self: center;
      max-width: 100px;
      border-radius: 7px;
      border: solid 1px grey;
    }
  }

</style>
