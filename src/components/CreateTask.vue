<template>
  <div class="flex justify-between align-center bg-neutral p-6 mb-5 rounded-lg shadow-2xl">
    <input type="text" class="input input-primary mr-2" v-model="taskDescription" placeholder="Descrição da tarefa..." />
    <button class="btn btn-primary" @click="createTask">
      <PhPlus color="#006724" weight="bold" />
      Criar
    </button>
  </div>
</template>

<script setup lang="ts">
import { defineEmits, ref } from 'vue'
import type { Task } from '../types/Task'
import { PhPlus } from '@phosphor-icons/vue'

const emit = defineEmits(['taskCreated'])

const taskDescription = ref()

function createTask() {
  const newTask: Task = {
    "id": Date.now(),
    "description": taskDescription.value,
    "done": false
  }

  emit('taskCreated', newTask)
  taskDescription.value = ''
}
</script>

<style scoped>
button {
  color: #006724;
}
</style>