<template>
  <div class="card w-md p-10 bg-neutral rounded-lg shadow-2xl">
    <div class="pb-6">
      <h1 class="text-xl font-medium">Lista de tarefas</h1>
    </div>
    <p v-if="!localTasks || localTasks.length === 0">Você ainda não tem tarefas para hoje...</p>
    <ul v-else>
      <li v-for="task in localTasks" :key="task.id">
        <input 
          class="checkbox checkbox-primary mr-2" 
          type="checkbox" 
          v-model="task.done" 
          @change="markTaskDone(task)" 
        />
        <span>{{ task.description }}</span>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import axios from 'axios'
import { defineProps, defineEmits, ref, watch } from 'vue'
import type { PropType } from 'vue'
import type { Task } from '../types/Task'

const props = defineProps({
  tasks: Array as PropType<Task[]>
})

const emit = defineEmits(['taskUpdated'])

const localTasks = ref<Task[]>(props.tasks ?? [])

watch(() => props.tasks, (newTasks) => {
  localTasks.value = [...(newTasks ?? [])]
}, { deep: true })

const markTaskDone = async (task: Task) => {
  try {
    await axios.put(`http://localhost:3000/tasks/${task.id}`, {
      ...task,
      done: task.done
    });
  } catch (error) {
    console.error("Erro ao atualizar tarefa:", error);
  }
}
</script>

<style scoped>
  h1, span {
    color: white;
  }

  p {
    color: var(--color-base-300);
  }
</style>