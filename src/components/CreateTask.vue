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
import axios from 'axios'
import type { Task } from '../types/Task'
import { PhPlus } from '@phosphor-icons/vue'

const emit = defineEmits(['taskCreated'])

const taskDescription = ref()

const createTask = async () => {
  const newTask: Task = {
    "id": Date.now(),
    "description": taskDescription.value,
    "done": false
  }

  try {
    await axios.post("http://localhost:3000/tasks", newTask);
    emit("taskCreated", newTask);
    taskDescription.value = "";
  } catch (error) {
    console.error("Error on create task: ", error);
  }
}
</script>

<style scoped>
button {
  color: #006724;
}
</style>