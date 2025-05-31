<script lang="ts" setup>
import { ref } from "vue";
import TaskForm from "./components/TaskForm.vue";
import type { Task } from "./types";

const message = ref("Tasks App");
const tasks = ref<Task[]>([]);

function addTask(newTask: string) {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false
  })
}

</script>

<template>
  <main>
    <h1>{{ message }}</h1>
    <TaskForm @add-task="addTask"/>
    <!-- If this Task form emits the add task event, call this function, use data -->
     <h3>There are {{ tasks.length }} tasks to complete.</h3>
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


<!-- Notes -->
 <!-- Adding scoped param to styles scopes those styles exculisvely 
  to the component that it's in, even if there is an element by 
  the same name -->
<!-- Setup keyword in Script makes for less boilerplate when making the 
  component -->
<!-- ref is imported from vue and is how we define reactive state values -->
 <!-- This is known as an SFC, single file component since the script,
  template and styles are all in this component -->
<!-- In order to bind the input to the state variable use v-model-->
<!-- To add a DOM event to an element you can use the @ sign.  
  If you want to reference the current value of the form, you need to
  append .value. The state variable is essentially an object wrapper around
  a primitive. Prevent default action by appending .prevent on submit action -->
<!-- Preferred way in vue to pass state up is to emit an event -->


