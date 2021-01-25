<template>
  <h1>Vue 3 TODO APP</h1>
  <form @submit.prevent="addNewTodo">
    <label>New Todo</label>
    <input v-model="newTodo" name="newTodo" />
    <button>Add new Todo</button>
  </form>
  <button @click="removeAllTodos">Remove All</button>
  <button @click="markAllDone">Mark all done</button>
  <ul>
    <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
      <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
        {{ todo.content }}
      </h3>
      <button @click="removeTodo(index)">Remove todo</button>
    </li>
  </ul>
</template>

// :class="{ done: todo.done }" says if todo.done === true apply styling to
class done

<script>
import { ref } from "vue";

export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]); //created an array of todos

    function addNewTodo() {
      todos.value.push({
        id: Date.now(), //normally dont use Date.now for id !
        done: false,
        content: newTodo.value,
      }); // When function is called pushed object in the todos array !
      newTodo.value = ""; // So the input field is empty after button is clicked !
    }

    function toggleDone(todo) {
      todo.done = !todo.done;
    }

    function removeTodo(index) {
      todos.value.splice(index, 1);
    } // This function will now remove 1 specific element of that index

    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }

    function removeAllTodos() {
      todos.value = []; //Removes all todos by setting array to empty
    }

    return {
      newTodo,
      addNewTodo,
      todos,
      toggleDone,
      removeTodo,
      markAllDone,
      removeAllTodos,
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

.todo {
  cursor: pointer;
}

.done {
  text-decoration: line-through;
}
</style>
