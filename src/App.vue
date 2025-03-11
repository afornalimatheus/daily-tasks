<template>
  <header></header>
  <main>
    <div class="mx-auto flex items-center justify-center max-w-full min-h-screen max-h-full bg-base">
      <div>
        <!-- Component that emit event -->
        <CreateTask @taskCreated="updateListTasks" />
        <ListTasks :tasks="tasks"/>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import axios from 'axios'
import type { Task } from './types/Task'
import ListTasks from './components/ListTasks.vue'
import CreateTask from './components/CreateTask.vue'

const tasks = ref<Task[]>([])

onMounted(() => {
  axios.get<Task[]>("http://localhost:3000/tasks")
    .then((response) => {
      console.log(response.data)
      tasks.value = response.data
    })
    .catch((error) => {
      console.error("Erro: ", error)
    })
})
</script>

<style scoped>
</style>
