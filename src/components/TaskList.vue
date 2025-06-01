<script lang="ts" setup>
import type { Task } from "../types";

const props = defineProps<{ 
    tasks: Task[] 
}>();

const emits = defineEmits<{
    toggleDone: [id: string]
}>();

</script>

<template>
    <div class="task-list">
        <article v-for="task in props.tasks" :key="task.id">
            <label>
                <input 
                type="checkbox"
                :checked="task.done"
                @input="emits('toggleDone', task.id)"
                >
                {{ task.title }}
            </label>
        </article>
    </div>
</template>

<style>
    .task-list {
        margin-top: 1rem;
    }
    </style>
    <!-- v-model binds the input to task.done. While you can do this,
     it's best practive to only modify state where it's defined, 
     so we instead will use emits-->