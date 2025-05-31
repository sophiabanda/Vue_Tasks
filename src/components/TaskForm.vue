<script lang="ts" setup>
import { ref } from "vue";

const emit = defineEmits<{
    addTask: [newTask: string]
}>()

const newTask = ref("");

function formSubmitted() {
  if (newTask.value.trim()) {
    emit("addTask", newTask.value.trim());
    newTask.value ="";
  }
}
</script>

<template>
     <form @submit.prevent="formSubmitted">
      <label>New Task</label>
      <input v-model="newTask" name="newTask">
      <div class="button-container">
        <button>Add</button>
      </div>
    </form>
    <h3>{{ newTask }}</h3>
</template>