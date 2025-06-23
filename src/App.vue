<script setup lang="ts">
import { computed, ref } from 'vue';
import type { Task } from './types';
import TaskForm from './components/TaskForm.vue';
import TaskList from './components/TaskList.vue';

const tasks = ref<Task[]>([]);
const totalCompleted = computed(() => tasks.value.filter(t => t.completed).length);

const addTask = (newTask: string) => {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    completed: false,
  });
};

const removeTask = (taskId: string) => {
  tasks.value = tasks.value.filter((task) => task.id !== taskId);
}

const toggleComplete = (taskId: string) => {
  const task = tasks.value.find((task) => task.id === taskId);
  if (task) {
    task.completed = !task.completed;
  }
};
</script>

<template>
  <main>
    <h1>Hello World</h1>

    <!-- listen for the addTask event from this component -->
    <TaskForm @add-task="addTask" />

    <div v-if="!tasks.length">Add a task to get started!</div>
    <div v-else>{{ totalCompleted }} / {{ tasks.length }} Tasks Completed</div>

    <TaskList
      :tasks="tasks"
      @toggle-complete="toggleComplete"
      @remove-task="removeTask"
    />
  </main>
</template>

<style scoped>
main {
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  padding: 1rem;
}

form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}
</style>
