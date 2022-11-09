<template>
  <div>
      <textarea
        v-model="todoBody"
        type="text"
      />
    <div>
      {{ date }}
    </div>
    <div>
      <button @click="changeCompleted">
        DONE
      </button>
      <button @click="$emit('remove', id)">
        DELETE
      </button>
    </div>
  </div>
</template>

<script setup>
  import {toRefs} from "vue";

  defineEmits([
    'remove',
  ])

  const props = defineProps({
    todo: {
      type: Object,
      required: true,
    }
  })

  const {todo: todoBody, date, completed, id} = toRefs(props.todo)

  const changeCompleted = () => {
    completed.value = !completed.value
  }

</script>

<style lang="scss" scoped>
  .todo-list__item {
    textarea {
      border: none;
      outline: none;
      resize: none;
      overflow: visible;
      font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
      font-size: 16px;
      line-height: 24px;
      font-weight: 400;
      min-height: 100px;
    }

    button {
      max-width: 200px;
      min-width: 105px;
      border: solid 1px silver;
    }

    button:nth-child(odd) {
      color: deeppink;
      border: solid 1px deeppink;
    }

    &.completed {
      position: relative;

      &:after {
        content: "";
        position: absolute;
        display: block;
        width: 100%;
        height: 5px;
        top: 35%;
        left: 0px;
        background: #1a1a1a;
      }
    }
  }
</style>
