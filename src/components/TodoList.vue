<template>
  <ul class = "todolist">
    <li v-for = "todo in array" key="todo.id">
      <p>{{todo.todo}}</p>
      <p>{{todo.date}}</p>
      <button class="purple">EDIT</button>
      <button class="red" @click="$emit('done',todo)">DONE</button>
      <button class="grey" @click="$emit('remove',todo)">DELETE</button>
    </li>
  </ul>
</template>

<script setup>
defineProps({
  array:Array
})



</script>

<style scoped>
ul{
  list-style-type:none;
  padding: 0px;
}
li{
  padding: 0px;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
li p{
  max-width: 150px;
  min-width: 105px;
}
ul button{
  max-width: 75px;
  max-width: 100px;

}
.red{
  color: deeppink;
  border: solid 1px deeppink;
}
.purple{
  color: #646cff;
  border: solid 1px #646cff;
}
.grey{

  border: solid 1px  silver;
}

</style>
