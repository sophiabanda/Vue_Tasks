<script lang="ts" setup>
import { ref, computed } from "vue";
import TaskForm from "./components/TaskForm.vue";
import TaskList from "./components/TaskList.vue"
import type { Task } from "./types";

const message = ref("Tasks App");
const tasks = ref<Task[]>([]);
// 'typed' in separate file

const totalDone = computed(() => tasks
.value
.reduce((total, task) => task.done ? total + 1 : total, 0));
//Compostion function: computed(), imported from vue. Accepts callback
// whatever it returns will get stored in this variable (tasks) as a
//reactive variable. If any dependencies change it will always have the
// latest value. Only runs if dependency changes!

function addTask(newTask: string) {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false
  });
}

function toggleDone(id: string) {
  const task = tasks.value.find((task) => task.id === id);
  if (task) {
    task.done = !task.done
  }
}

function removeTask(id: string) {
  const index = tasks.value.findIndex((task) => task.id === id);
  if (index !== -1) {
    tasks.value.splice(index, 1)
  }
}

</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm @add-task="addTask"/>
    <!-- @ sign here allows us to tap into the event being emitted from 
     TaskForm.vue. If this Task form emits the add task event, 
     call this function, use data -->
     <h3 v-if="!tasks.length">Add a task to get started.</h3>
     <h3 v-else>{{  totalDone }} / {{ tasks.length }} tasks completed.</h3>
    <!-- Conditionally render the h3 with v-if -->
     <TaskList :tasks @toggle-done="toggleDone" @remove-task="removeTask"/>
  </main>
</template>

<style>
  main {
    max-width: 800px;
    margin: 1rem auto;
  }
  .button-container {
    display: flex;
    justify-content: end;
  }
</style>