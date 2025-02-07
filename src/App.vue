<script setup>
import UiButton from "@/components/UiButton.vue";
import TodoItem from "./components/TodoItem.vue";

import { ref } from "vue";

const count = ref(0);
const taskList = ref([]);
const addTask = () => {
  taskList.value.push({
    id: 'id' + Math.floor(Math.random() * 1000),
    name: '',
    text: '',
    date: '',
    status: 'WAITING',
  })
}

const deleteTask = (taskId) => {
  taskList.value = taskList.value.filter((task) => task.id !== taskId)
  console.log(`DELETED TASK WITH ID === ${taskId}`)
}

const modTask = (
    taskId,
    taskName,
    taskText,
    taskDate,
    isSaved
) => {
  for (const task of taskList.value) {
    if (task.id === taskId) {
      task.name = taskName
      task.text = taskText
      task.date = taskDate
      task.status = isSaved ? 'SAVED' : 'NOT-SAVED'
    }
  }
}
const clearTaskList = () => {
  taskList.value = []
}

const changeColor = () => {
  const root = document.documentElement;
  root.style.setProperty("--hue", Math.floor(Math.random() * 360));
};
</script>

<template>
  <div class="main-container">
    <div class="title-bar-container">
      <h1>Todo List</h1>
      <div class="title-bar-buttons">
        <UiButton button-type="TITLE" @action="addTask">add</UiButton>
        <UiButton button-type="TITLE" @action="clearTaskList">clear</UiButton>
        <UiButton button-type="TITLE" @action="changeColor">color</UiButton>
      </div>
    </div>
    <div>{{ taskList }}</div>
    <div class="todo-items-container">
      <TodoItem v-for="task in taskList" :key="task.id" :todo-item="task"
      @delete-task="deleteTask"
      @mod-task="modTask"/>
    </div>
  </div>
</template>

<style scoped>
.main-container {
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
</style>
