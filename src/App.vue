<template>

<div class="min-h-screen flex flex-col justify-center items-center">

<header class="flex flex-col w-full container">

<h1 class="text-6xl font-light text-gray-800 text-center">My To Do App</h1>
<input 
class="text-3xl py-2 px-4 rounded-xl w-full text-gray-800  mt-8" 
type="text" 
placeholder="New Todo" 
v-model="newTodo" 
@change="addTodo"
/>

</header>
<main class="w-full mt-16 container space-y-8">
  <section class="space-y-4" v-if="pendingTodos.length >0">
<h3 class="text-3xl font-thin text-green-800">Pending Items: {{pendingTodos.length}}</h3>
<ul class="space-y-4">
  <li v-for="todo in pendingTodos" :key="todo.id"  class="bg-white rounded-xl text-2xl py-2 px-4 font-light text-green-800 text-center hover:text-white hover:bg-green-800 cursor-pointer transition-colors" @click="changeStatus(todo.id)">
    {{todo.text}}</li>
</ul>
  </section>

<section class="space-y-4" v-if="completedTodos.length >0">
<h3 class="text-3xl font-thin text-red-800">Completed Items: {{completedTodos.length}}</h3>
<ul class="space-y-4">
  <li v-for="todo in completedTodos" :key="todo.id" class="bg-white rounded-xl text-2xl py-2 px-4 font-light text-red-800 text-center hover:text-white hover:bg-red-800 cursor-pointer transition-colors" @click="changeStatus(todo.id)">
    {{todo.text}}</li>
</ul>
</section>

</main>
</div>
</template>

<script setup>
import {ref, computed} from 'vue'

const newTodo = ref('')

const todos = ref([])

const pendingTodos = computed(()=>
 todos.value.filter(todo => todo.status === 'pending'),
)

const completedTodos = computed(()=>
 todos.value.filter(todo => todo.status === 'done'),
)

const changeStatus = id => {
  todos.value.map(todo=>
  {if(todo.id === id){
    todo.status = todo.status === 'pending' ? 'done' : 'pending'
}
})
}

const addTodo = () =>{
  if(newTodo.value.length>0){
    todos.value.push({
      id: todos.value.length,
      text: newTodo.value,
      status: 'pending',
    })
    newTodo.value=''
  }
}

</script>

