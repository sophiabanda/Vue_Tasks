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
        <article class="task" v-for="task in props.tasks" :key="task.id">
            <label>
                <input 
                type="checkbox"
                :checked="task.done"
                @input="emits('toggleDone', task.id)"
                >
                <span :class="{ done: task.done }">{{ task.title }}</span>
            </label>
            <button class="outline">Remove</button>
        </article>
    </div>
</template>

<style>
    .task-list {
        margin-top: 1rem;
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