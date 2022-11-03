<template>

<ul class="todolist__done">
  <li v-for = "todoDone in arrayDone">
    <p>{{todoDone.todo}}</p>
    <p>{{todoDone.date}}</p>
    <button>DONE</button>
    <button>DELETE</button>
  </li>
</ul>

</template>

<script setup>
  defineProps({
  arrayDone:Array
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
    background: cadetblue;
    position: relative;
    border-radius: 5px;
    opacity: 0.6;
    margin: 10px 0px;
    border: solid 1px grey;
    border-radius: 5px;
  }

  li p{
    max-width: 200px;
    min-width: 105px;
  }

  li button{
    background: cadetblue;
    max-width: 75px;
    max-width: 100px;
  }
  li:after{
    content: "";
    position: absolute;
    display: block;
    width: 500px;
    height: 5px;
    top: 50%;
    left: 0px;
    background: #1a1a1a;

  }
</style>
