<template>
  <h1 style="text-align: center;">TO DO LIST</h1>
  <hr />
  <form action="" @submit.prevent="addTodo">
    <fieldset role="group">
      <input v-model="newTodo" type="text" placeholder="Tâche à effectuer" />
      <button :disabled="newTodo.length === 0">Ajouter</button>
    </fieldset>
  </form>
  <div v-if="todos.length === 0">Vous n'avez pas de tâches à faire</div>
  <div v-else>
    <ul>
      <li v-for="todo in sortedTodos()" :key="todo.date" :class="{completed: todo.completed}">
        <label>
          <input type="checkbox" v-model="todo.completed" />
          {{ todo.title }}
        </label>
      </li>
    </ul>
    <label>
      <input type="checkbox" v-model="hideCompleted"> Masquer les tâches complétées
    </label>
  </div>
</template>

<script setup>
import { ref } from "vue";
const hideCompleted = ref(false)
const newTodo = ref("");
const todos = ref([
  {
    title: "Tâche réalisé",
    completed: true,
    date: 1,
  },  
  
  {
    title: "Tâche à faire",
    completed: false,
    date: 2,
  },
]);

const addTodo = () => {
  todos.value.push({
    title: newTodo.value,
    completed: false,
    date: Date.now(),
  });
  newTodo.value = "";
};


const sortedTodos = () => {
const x =  todos.value.toSorted((a,b)=>a.completed > b.completed ? 1: -1)
if (hideCompleted.value === true ) {
  return x.filter (t => t.completed === false)
}
return x
}
</script>

<style>

.completed{

  opacity: 50%;
  text-decoration: line-through;
}
</style>
