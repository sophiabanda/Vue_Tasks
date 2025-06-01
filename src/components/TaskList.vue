<script lang="ts" setup>
import type { Task } from "../types";

const props = defineProps<{ 
    tasks: Task[] 
}>();

const emits = defineEmits<{
    toggleDone: [id: string];
    removeTask: [id: string];
}>();

</script>

<template>
        <TransitionGroup name="task-list" tag="div" class="task-list">
            <article class="task" v-for="task in props.tasks" :key="task.id">
                <label>
                    <input 
                    type="checkbox"
                    :checked="task.done"
                    @input="emits('toggleDone', task.id)"
                    >
                    <span :class="{ done: task.done }">{{ task.title }}</span>
                </label>
            <button @click="emits('removeTask', task.id)" class="outline">Remove</button>
        </article>
    </TransitionGroup>
</template>

<style>
    .task-list {
        margin-top: 1rem;
    }

    .task-list-enter-active,
    .task-list-leave-active {
        transition: all 0.5s ease;
    }
    .task-list-enter-from,
    .task-list-leave-to {
        opacity: 0;
        transform: translateX(30px);
    }

    .task {
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .done {
        text-decoration: line-through;
    }
</style>
    <!-- v-model binds the input to task.done. While you can do this,
     it's best practive to only modify state where it's defined, 
     so we instead will use emits-->