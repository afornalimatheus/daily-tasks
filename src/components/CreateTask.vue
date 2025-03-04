<template>
  <div class="flex justify-between align-center bg-neutral p-6 mb-5 rounded-lg shadow-2xl">
    <input type="text" class="input input-primary" v-model="taskDescription" placeholder="Descrição da tarefa" />
    <button class="btn btn-primary" @click="createTask">Criar</button>
  </div>
</template>

<script setup lang="ts">
import { defineEmits, ref } from 'vue'
import type { Task } from '../types/Task'

const emit = defineEmits(['taskCreated'])

const taskDescription = ref()

function createTask() {
  const newTask: Task = {
    "id": Date.now(),
    "description": taskDescription.value,
    "done": false
  }

  emit('taskCreated', newTask)
}
</script>

<style scoped>
button {
  color: #006724;
}
</style>