<template>
  <h1>Vue 3 Composition API TODO APP</h1>
  <form @submit.prevent="addTodo">
    <label for="newTodo">TODO : </label>
    <input type="text" name="newTodo" v-model="newTodo" />
    <button>Add</button>
  </form>
  <!-- <h2>{{ newTodo }}</h2> -->
  <button @click="removeAll()">Remove All</button>
  <button @click="markAllDone()">All Done</button>
  <center>
    <table class="center">
      <tr v-for="(todo, index) in todos" :key="todo.in" class="todo">
        <td><h4 :class="{ done : todo.done }" @click="toggleDone(todo)">{{ todo.content }} </h4></td>
        <td><button @click="removeTodo(index)">x</button></td>
      </tr>
    </table>
  </center>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    function addTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }

    function toggleDone(todo){
      todo.done = !todo.done;
    }
    function removeTodo(index){
      if(confirm(`Remove ${index} ?`)){
        todos.value.splice(index, 1);
      }
    }

    function markAllDone(){
      todos.value.forEach((todo)=>todo.done=true)
    }

    function removeAll(){
      if(confirm("Remove ALL ?")){
        todos.value=[];
      }
    }
    return { newTodo, addTodo, todos, toggleDone, removeTodo, markAllDone, removeAll };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.done{
  text-decoration: line-through;
}
.todo{
  cursor: pointer;
}
</style>
