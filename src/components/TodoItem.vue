<template>


    <li v-for = "todo in todos" :key="todo.id" :class="{'completed':todo.completed == true}" >
      <textarea type="text"
             :value="todo.todo"
             @input="todo.todo = $event.target.value"/>
      <p>{{todo.date}}</p>
      <button class="red" @click="$emit('done',todo)">DONE</button>
<!--      <button class="red" @click="selectCurrentTodod(todo,todos)">DONE</button>-->
      <button class="grey" @click="$emit('remove',todo)">DELETE</button>
    </li>

</template>

<script setup>
import {ref, computed} from "vue";

defineProps({
  todos:Array
})
const currentTodo = ref({})
const completedTodo = computed( () => {
return  [1,2,3]
})
const selectCurrentTodod = (todo,todos) => {
  console.log(todo, todos)
  currentTodo.value = todo
  console.log(currentTodo.value)
}




</script>

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
      width: 500px;
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
//  .completed{
//
//
//  }
//.completed:after{
//    content: "";
//    position: absolute;
//    display: block;
//    width: 500px;
//    height: 5px;
//    top: 20%;
//    left: 0px;
//    background: #1a1a1a;
//  }
//ul{
//  list-style-type:none;
//  padding: 0px;
//}
//li{
//  padding: 0px;
//  display: flex;
//  align-items: flex-start;
//  margin: 10px 0px;
//  border-radius: 5px;
//}
//textarea{
//  display: block;
//  border:none;
//  outline: none;
//  resize: none;
//  justify-content: flex-start;
//  overflow: visible;
//  font-family: Inter, Avenir, Helvetica, Arial, sans-serif;
//  font-size: 16px;
//  line-height: 24px;
//  font-weight: 400;
//  min-height: 100px;
//}
//li p{
//  max-width: 200px;
//  min-width: 105px;
//}
//ul button{
//  max-width: 75px;
//  max-width: 100px;
//}
//.red{
//  color: deeppink;
//  border: solid 1px deeppink;
//}
//.purple{
//  color: #646cff;
//  border: solid 1px #646cff;
//}
//.grey{
//
//  border: solid 1px  silver;
//}

</style>
