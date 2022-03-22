<template>
  <div class="list">
    <h1>What's the plan for today?</h1>
    <form @submit.prevent="addNewTodo">
      <input v-model="newTodo" name="newTodo" placeholder="Add a todo"/>
      <button class="add-btn">Add Todo</button>
    </form>
    <button class="options" @click="removeAllTodos">Remove All</button>
    <button class="options" @click="markAllDone">Mark All Done</button>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id" class="todo">
        <h3 :class="{ done: todo.done }" @click="toggleDone(todo)">
          {{ todo.content }}
        </h3>
        <button class="btn-remove" @click="removeTodo(index)">X</button>
      </li>
    </ul>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  setup() {
    const newTodo = ref("");
    const todos = ref([]);
    function addNewTodo() {
      todos.value.push({
        id: Date.now(),
        done: false,
        content: newTodo.value,
      });
      newTodo.value = "";
    }
    function toggleDone(todo) {
      todo.done = !todo.done;
    }
    function removeTodo(index) {
      todos.value.splice(index, 1);
    }
    function markAllDone() {
      todos.value.forEach((todo) => (todo.done = true));
    }
    function removeAllTodos() {
      todos.value = [];
    }
    return {
      todos, newTodo,
      addNewTodo, toggleDone,
      removeTodo, markAllDone,
      removeAllTodos,
    };
  },
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  background: linear-gradient(
    90deg,
    rgba(48, 16, 255, 1) 0%,
    rgba(100, 115, 255, 1) 100%
  );
  color: white;
}
.list {
  text-align: center;
  background: #161a2b;
  width: 600px;
  margin: 128px auto;
  padding: 40px;
  border-radius: 30px;
}
input {
  padding: 14px 32px 14px 16px;
  border-radius: 4px 0 0 4px;
  border: 2px solid #5d0cff;
  outline: none;
  width: 320px;
  background: transparent;
  color: #fff;
  
}
.options,.add-btn {
    padding: 16px;
  border: none;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
  outline: none;
  background: linear-gradient(
    90deg,
    rgba(93, 12, 255, 1) 0%,
    rgba(155, 0, 250, 1) 100%
  );
  color: #fff;
  text-transform: capitalize;
}
.btn-remove {
  background-color: transparent;
  border: none;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
  outline: none;
  color: white;
  font-size: 30px;
  position: absolute;
  left: 470px;
  top: 15px;
}

.options {
    margin-left: 5px;
    margin-right: 5px;
    border-radius: 10px;
}

h1, input, .options {
  margin-bottom: 20px;
}
li {
  list-style-type: none;
}
.todo {
  position: relative;
  cursor: pointer;
  margin-bottom: 10px;
  border-radius: 10px;
  padding-top: 17px;
  padding-bottom: 17px;
  font-size: 20px;

   background: linear-gradient(
    90deg,
    rgba(255, 118, 20, 1) 0%,
    rgba(255, 84, 17, 1) 100%
  );
}
.todo:nth-child(4n + 1) {
  background: linear-gradient(
    90deg,
    rgba(93, 12, 255, 1) 0%,
    rgba(155, 0, 250, 1) 100%
  );
}

.todo:nth-child(4n + 2) {
  background: linear-gradient(
    90deg,
    rgba(255, 12, 241, 1) 0%,
    rgba(250, 0, 135, 1) 100%
  );
}

.todo:nth-child(4n + 3) {
  background: linear-gradient(
    90deg,
    rgba(20, 159, 255, 1) 0%,
    rgba(17, 122, 255, 1) 100%
  );
}

.done {
  text-decoration: line-through;
}

</style>
