<template>
  <div class="card w-md p-10 bg-neutral rounded-lg shadow-2xl">
    <div class="pb-6">
      <h1 class="text-xl font-medium">Lista de tarefas</h1>
    </div>
    <p v-if="!tasks || tasks.length === 0">Não tem tarefas</p>
      <ul v-else>
        <li v-for="task in tasks" :key="task.id">
          <input class="checkbox checkbox-primary mr-2" type="checkbox" />
          <span>{{ task.description }}</span>
        </li>
      </ul>
  </div>
</template>

<script setup lang="ts">
import { defineProps } from 'vue'
import type { PropType } from 'vue'
import type { Task } from '../types/Task'

defineProps({
  tasks: Array as PropType<Task[]>
})

</script>

<style scoped>
  h1, span {
    color: white;
  }
</style>