<template>
  <div>
      <textarea type="text"
                v-model="item.todo"
      />
    <p>{{ item.date }}</p>
    <button @click="$emit('changeCompleted', item)">DONE</button>
    <button @click="$emit('remove', item)">DELETE</button>
  </div>
</template>

<script setup>
  const emit = defineEmits([
    'remove',
    'changeCompleted'
  ])

  defineProps({
    item: Object
  })

</script>


<style lang="scss" scoped>
  .todo-list__item {
    textarea {
      grid-row: 1/3;
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
    }

    button {
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
        top: 20%;
        left: 0px;
        background: #1a1a1a;
      }
    }
  }
</style>
