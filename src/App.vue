<script setup>
import UiButton from "@/components/UiButton.vue";
import TodoItem from "./components/TodoItem.vue";

import { ref } from "vue";

const taskCount = ref(0);
const taskList = ref([]);
const addTask = () => {
  taskList.value.push({
    id: 'id' + Math.floor(Math.random() * 1000),
    name: '',
    text: '',
    date: '',
    status: 'WAITING',
  })
  taskCount.value++
}

const deleteTask = (taskId) => {
  taskList.value = taskList.value.filter((task) => task.id !== taskId)
  taskCount.value--
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
  taskCount.value = 0
}

const changeColor = () => {
  const root = document.documentElement;
  root.style.setProperty("--hue", Math.floor(Math.random() * 360))
};
</script>

<template>
  <div class="main-container">
    <div class="title-bar-container">
      <div class="title-container">
        <div v-if="taskCount" class="counter-container">{{ taskCount }}</div>
        <h1 class="title">tasks</h1>
      </div>
      <div class="title-bar-buttons">
        <UiButton button-type="TITLE" @action="addTask">add</UiButton>
        <UiButton v-if="taskCount" button-type="TITLE" @action="clearTaskList">clear</UiButton>
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

.title-container {
  min-width: 8rem;
  display: flex;
  justify-content: space-evenly;
  border: var(--border-container);
}

.title,
.counter-container  {
  font-size: 1.5rem;
  font-family: monospace;
  font-weight: bold;
  color: var(--main-color-darker);
  border: var(--border-sub-container);
}

.title-bar-buttons {
  min-width: 15rem;
  display: flex;
  justify-content: space-between;
  gap: 1rem;
  border: var(--border-sub-container);
}

</style>
