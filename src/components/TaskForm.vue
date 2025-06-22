<script setup lang="ts">
import { ref } from 'vue';

// instead of using props, we can use emits to emit events to the parent component
// this is the preferred way to communicate with the parent component
const emit = defineEmits<{
    addTask: [newTask: string]
}>();

const newTask = ref('');
const error = ref('');

const onSubmit = () => {
    if (!newTask.value.trim()) {
        error.value = 'Task cannot be empty';
        return;
    }

    // emit the addTask event with the newTask value
    emit('addTask', newTask.value.trim());
    newTask.value = '';
};
</script>


<template>
    <form @submit.prevent="onSubmit">
        <div class="form-group">
            <label for="newTask">New Task</label>
            <input
                type="text"
                id="newTask"
                v-model="newTask"
                :aria-invalid="!!error || undefined"
                @input="error = ''"
            />
            <!-- show the error message if there is an error -->
            <p v-if="error" class="error">{{ error }}</p>
        </div>

        <button type="submit">Add Task</button>
    </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  width: 100%;
}

.form-group {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 0.25rem;
  width: 100%;
}

.form-group label {
  font-weight: bold;
}

.form-group input {
  width: 100%;
}
</style>