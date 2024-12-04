<script setup>
import AddButton from './components/AddButton.vue';
import ClearButton from './components/ClearButton.vue';
import TodoItem from './components/TodoItem.vue';

import { ref } from 'vue';

const count = ref(0)

const changeColor = () => {
  const root = document.documentElement
  root.style.setProperty('--hue', Math.floor(Math.random() * 360))
}
</script>

<template>
  <div class="main-containter">
    <div class="title-bar-container">
      <h1>Todo List</h1>
      <div class="title-bar-buttons">
        <AddButton @add-task="count++" />
        <ClearButton @clear-tasks="count = 0" />
        <button @click="changeColor">discoteka</button>
      </div>
    </div>
    <div class="todo-items-container">
      <TodoItem v-for="index in count" :key="index" />
    </div>
  </div>
</template>

<style scoped>
.main-containter {
  width: 100vw;
  min-width: 17rem;
  display: flex;
  flex-direction: column;
  border: var(--border-main-container);
}

.todo-items-container {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: start;
  gap: 1rem;
  padding: 1rem;
  border: var(--border-container);
}

.title-bar-container {
  display: flex;
  flex-flow: row wrap;
  justify-content: center;
  align-items: center;
  gap: 1.5rem;
  padding: 1rem;
  border: var(--border-container);
  background-color: var(--main-color-very-light-mod);
}

h1 {
  font-family: monospace;
  font-weight: bold;
  color: var(--main-color-darker);
  border: var(--border-sub-container);
}

.title-bar-buttons {
  display: flex;
  gap: 1rem;
  border: var(--border-sub-container);
}

button {
  font-size: 1rem;
  font-weight: bold;
  cursor: pointer;
  border: none;
  background-color: var(--main-color-text);
  color: var(--main-color-darker);
  border: var(--border-button);
  border-radius: var(--main-radius);
  box-shadow: var(--main-shadow);
  padding: .5rem 1rem;
  transition: .3s;
  text-transform: lowercase;
}

button:hover {
  background-color: var(--main-color);
  color: var(--main-color-text);
}

button:active {
  background-color: var(--main-color-text);
  color: var(--main-color-darker);
}
</style>