<script setup>
import { ref, reactive } from 'vue';
let todos = [
  { id: 1, name: 'coding', isDone: true },
  { id: 2, name: 'reading', isDone: true },
  { id: 3, name: 'walking', isDone: false },
  { id: 4, name: 'watching', isDone: false },
];
const todosLi = ref(todos);
//const todosLi = reactive(todos);
const newTodo = ref('');
const handleAdd = () => {
  todos.push({ id: todos.length + 1, name: newTodo.value, isDone: false });
  // console.log(todos);
  newTodo.value = '';
};
const handleDelete = (id) => {
  console.log(id);
  todos = todos.filter((todo) => todo.id !== id);
  console.log(todosLi);
  //todosLi = todosLi.filter((todo) => todo.id !== id); //not arry but an obj
  //delete todosLi[id - 1]; //? not rending
  //nextTick(() => {});
  todosLi.value = todosLi.value.filter((todo) => todo.id !== id);
};
</script>

<template>
  <div class="container">
    <h3>Todo List</h3>
    <div>
      <input v-model="newTodo" placeholder="add a task" />
      <button @click="handleAdd">Add</button>
      <!-- <p>{{ newTodo }} unwrapping</p> -->
    </div>
    <ul>
      <li v-for="todo in todosLi" :key="todo.id">
        {{ todo.name }} <button @click="handleDelete(todo.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
}
.container ul {
  list-style: none;
}
</style>
