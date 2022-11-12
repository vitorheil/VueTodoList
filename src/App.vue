<template>

  <div class="w-full h-screen bg-white ">
    <div class="border-1 bord-black rounded-2xl w-3/6 bg-violet-800 text-cyan-400 m-auto mt-32">
    <section class="h-16 text-2xl w-3/5 border-1 bord-black rounded-2xl">
      <h2 class="ml-5 p-3">Bem vindo<input class="bg-violet-800 text-cyan-400 ml-4 " type="text" placeholder="Nome" v-model="name"> </h2>
    </section>

    <section class="border-1 bord-black rounded-xl" >   
        <form class="text-cyan-400 text-center " @submit.prevent="addTodo">
          <h3 class="text-xl p-2 ">Adicione um Item</h3>
              <input
              class="mb-5 border-cyan-400 border-2 bg-violet-800 rounded-xl w-5/6 ml-4 p-1" 
              type="text" 
              placeholder="Adicione aqui" 
              v-model="inputContent">
            <!-- <h4 class="mb-2 text-xl">Escolha a categoria</h4>
          <div class="flex justify-center mr-12 mb-5 mt-5">
            <label class="w-32  bg-blue-500 mx-8 rounded-xl">
              <span class="rounded-xl bg-blue-900">
              <input 
              type="radio" 
              name="category"  
              value="bussines" 
              v-model="inputCategory"
              class="w-5"
              >
              </span>
              <div class="text-violet-800 text-base font-semibold">Bussines</div>
            </label>

            <label class="w-32 bg-fuchsia-700 text-center rounded-xl">
              <span class="rounded-xl border-pink-500 border-2 bg-pink-500">
              <input 
              type="radio" 
              name="category"  
              value="personal" 
              v-model="inputCategory"
              class="w-5"
              >
              </span>
              <div class="text-base font-semibold">Personal</div>
            </label>
          </div> -->
          <button type="submit" value="Add todo" class="border-2 rounded-xl border-cyan-400 p-1 mb-4">Adicionar Tarefas</button>
        </form>
    </section>

    <section class="h-10 bg-violet-600 rounded-xl h-full">
      <h3 class="text-2xl mx-8">Para fazer</h3>
      <div class="h-16">
        <div class="flex p-5 bg-violet-600 " v-for="todos in todosAsc" :key="todos" >
          <!-- <label class="mx-8">
            <span class="">
            <input class="" type="radio" v-model="todos.done">
            </span>
          </label>  -->

          <div class="">
            <input class=" bg-violet-700 rounded-xl p-1 w-96 text-center ml-16" type="text" v-model="todos.content">
          </div>

          <div class="ml-28 w-36 text-cyan-400 border-cyan-400 p-1 border-2 rounded-xl text-center">
            <button @click="removeTodo(todos)">Deletar</button>
          </div>

        </div>
      </div>
    </section>
    </div>
  </div>

</template>

<script setup lang="ts">
import {ref, onMounted, computed, watch} from 'vue'

const todo = ref([])
const name = ref('')
const inputContent = ref('')
const inputCategory = ref(null)

const todosAsc = computed(() => todo.value.sort(() => {
    return 
}))

watch(todo, (newVal) =>{
  localStorage.setItem('todo', JSON.stringify(newVal))
}, {deep: true})

watch(name,(newVal) => {
  localStorage.setItem('name', newVal)
})

const addTodo = () => {
  if(inputContent.value.trim() === ''){
    return
  }
  todo.value.push({
    content: inputContent.value,
    category: inputCategory.value,
    done: false,
    editable:false,
    createdAt: new Date().getTime()
  })
  inputContent.value = ''
  inputCategory.value = null
}

const removeTodo = (todos) => {
  todo.value = todo.value.filter((t) => t !== todos)
}

onMounted(()=>{
  name.value = localStorage.getItem('name') || ''
  todo.value = JSON.parse(localStorage.getItem('todo' ))|| []
 
})
</script>

<style>

</style>