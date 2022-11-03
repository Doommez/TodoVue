<template>
  <div class="container-header">
    <h2>Task</h2>
    <h2>Action</h2>
  </div>

  <ul class = "todolist">
    <li v-for = "todo in array" key="todo.id">
      <textarea type="text"
             :value="todo.todo"
             @input="todo.todo = $event.target.value"/>
<!--      <p>{{todo.todo}}</p>-->
      <p>{{todo.date}}</p>
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
  .container-header{
    display: flex;
    justify-content: space-around;
  }
ul{
  list-style-type:none;
  padding: 0px;
}
li{
  padding: 0px;
  display: flex;
  align-items: flex-start;
  margin: 10px 0px;
  border-radius: 5px;
}
textarea{
  display: block;
  border:none;
  outline: none;
  resize: none;
  justify-content: flex-start;
  overflow: visible;
  font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
  font-size: 16px;
  line-height: 24px;
  font-weight: 400;
  min-height: 100px;
}
li p{
  max-width: 200px;
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
