<template>
  <h1>Bienvenue sur la todo list</h1>
  <form action="" @submit.prevent="addTodo">
    <input 
      type="text" 
      placeholder="ajouter une todo" 
      v-model="newTodo"
      class="form-control w-50 d-inline-block"
    />
    <button :disabled="newTodo.length === 0 || newTodo.trim() ===''" type="submit" class="btn btn-primary p-1 ms-2">Ajouter</button>
  </form>
  <p v-if="todos.length === 0">il n'y a pas de todos pour l'instant</p>
  <ul v-else>
    <li v-for="(todo,index) in sortedTodos" :key="todo.date" :class="{'text-decoration-line-through opacity-50':todo.completed}">
      {{ todo.title }} <input type="checkbox" :name="`todo${index}`" :id="`todo${index}`" v-model="todo.completed"/>
    </li>
  </ul>
  <label>
    <input type="checkbox" v-model="hideCompleted">
    Masquer les tâches complétées
  </label>
  <p v-if="remainingTodos > 0 "> {{ remainingTodos }} tâche{{remainingTodos > 1 ?'s':''}} à faire</p>
  
</template>

<script setup>
import { ref,computed } from "vue";
const todos = ref([
  {
    title: "faire les courses",
    date: 1545789562,
    completed: true,
  },
  {
    title: "sortir le chien",
    date: 1545789562,
    completed: false,
  },
  {
    title: "tondre la pelouze",
    date: 1545789562,
    completed: true,
  },
]);

const newTodo = ref('')

const addTodo = computed(()=>{
  todos.value.push({
    title:newTodo.value,
    date:Date.now(),
    completed:false
  })
  newTodo.value=""
})

const sortedTodos = computed(() =>{
  const sortedTodos = todos.value.toSorted((a,b) => a.completed > b.completed ? 1 : -1)
  if(hideCompleted.value){
    return sortedTodos.filter(t => t.completed === false)
  }
  return sortedTodos
})

const remainingTodos = computed(()=>{
  return todos.value.filter(t => t.completed === false).length
})

const hideCompleted = ref(false)

</script>

