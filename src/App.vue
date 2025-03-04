<template>
  <header></header>
  <main>
    <div class="mx-auto flex items-center justify-center max-w-full min-h-screen max-h-full bg-base">
      <div>
        <CreateTask @taskCreated="updateListTasks" />
        <ListTasks :tasks="tasks"/>
      </div>
    </div>
  </main>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { Task } from "./types/Task"
import ListTasks from "./components/ListTasks.vue"
import CreateTask from "./components/CreateTask.vue"

const tasks = ref<Task[]>([
  {
    "id": 1,
    "description": "Varrer a casa",
    "done": false
  },
  {
    "id": 2,
    "description": "Lavar o carro",
    "done": false
  },
  {
    "id": 3,
    "description": "Levar a Torrada passear",
    "done": false,
  }
])

function updateListTasks(newTask: Task) {
  console.log('NOVA TAREFAS ', newTask);
  tasks.value.push(newTask)
}
</script>

<style scoped>
</style>
