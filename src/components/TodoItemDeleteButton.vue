<script setup></script>

<template>
  <button type="button" class="todo-item-delete-button" @click="$emit('delete-task')" tabindex="-1"></button>
</template>

<style scoped>
button.todo-item-delete-button {
  padding: 0;
  margin: 0;
  width: 1.5rem;
  height: 1.5rem;
  border-radius: 50%;
  /* border-radius: var(--main-radius); */
}

button.todo-item-delete-button:after {
  content: "\00d7";
  font-weight: bold;
}
</style>