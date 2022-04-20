<template>
  <div>
    <h1>TodoList</h1>
    <form @submit.prevent="formSubmit">
      <label for="newTodo"></label>
      <input type="text" id="newTodo" v-model="newTodo" />
      <button type="submit">click</button>
    </form>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id">
        <h3 :class="{ classThrow: todo.done }" @click="toggleClass(todo)">
          {{ todo.content }}
        </h3>
        <button @click="removeTodo(index)">delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "App",
  setup() {
    const newTodo = ref("");
    const todos = ref([]);

    function formSubmit() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }
    function toggleClass(todo) {
      todo.done = !todo.done;
    }
    function removeTodo(index){
      todos.value.splice(index, 1)
    }

    return {
      newTodo,
      todos,
      formSubmit,
      toggleClass,
      removeTodo
    };
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
.classThrow {
  text-decoration: line-through;
}
</style>
