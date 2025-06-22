<script setup lang="ts">
import TaskForm from './components/TaskForm.vue';

const addTask = (newTask: string) => {
  console.log('new task added! ', newTask);
};
</script>

<template>
  <main>
    <h1>Hello World</h1>

    <!-- listen for the addTask event from this component -->
    <TaskForm @add-task="addTask" />
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
