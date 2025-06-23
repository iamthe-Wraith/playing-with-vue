<script setup lang="ts">
import type { Task } from '../types';

const props = defineProps<{
    tasks: Task[];
}>();

const emits = defineEmits<{
    toggleComplete: [taskId: string];
    removeTask: [taskId: string];
}>();
</script>

<template>
    <TransitionGroup name="task" tag="div">
        <article v-for="task in props.tasks" :key="task.id">
            <input
                :id="task.id"
                type="checkbox"
                v-model="task.completed"
                @input="emits('toggleComplete', task.id)"
            />
            
            <label :for="task.id">
                {{ task.title }}
            </label>

            <button @click="emits('removeTask', task.id)">
                Remove
            </button>
        </article>
    </TransitionGroup>
</template>

<style scoped>
article {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    gap: 0.5rem;
}

article:has(input:checked) label {
    text-decoration: line-through;
}

label {
    flex-grow: 1;
    text-align: left;
}

.task-enter-active,
.task-leave-active {
    transition: all 0.5s ease;
}

.task-enter-from,
.task-leave-to {
    opacity: 0;
}
</style>