<script setup lang="ts">
import type { Task } from '../types';

const props = defineProps<{
    tasks: Task[];
}>();

const emits = defineEmits<{
    toggleComplete: [taskId: string];
}>();
</script>

<template>
    <article v-for="task in props.tasks" :key="task.id">
        <input
            type="checkbox"
            v-model="task.completed"
            @input="emits('toggleComplete', task.id)"
        />
        <h2>{{ task.title }}</h2>
    </article>
</template>

<style scoped>
article {
    display: flex;
    align-items: center;
    gap: 0.5rem;
}
</style>