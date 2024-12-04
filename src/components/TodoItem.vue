<script setup>
import TodoItemDeleteButton from './TodoItemDeleteButton.vue';
import TodoItemEditButton from './TodoItemEditButton.vue';

import TodoItemSaveButton from './TodoItemSaveButton.vue';

import { ref } from 'vue'

const taskName = ref()
const taskText = ref()
const taskDate = ref()


const isNotDeleted = ref(true)
const isNotSaved = ref(true)
const isNotEdited = ref(false)
const isColorModified = ref(false)

const deleteTask = () => {
  isNotDeleted.value = false
}

const saveTask = () => {
  isNotSaved.value = false
  isNotEdited.value = true
  isColorModified.value = !isColorModified.value
}

const editTask = () => {
  isNotEdited.value = false
  isNotSaved.value = true
  isColorModified.value = !isColorModified.value
}
</script>

<template>
  <div class="todo-item-container" v-if="isNotDeleted" :class="{ modColor: isColorModified }">
    <div class="todo-item-top">
      <input type="text" name="taskTitle" class="todo-item-name-input" placeholder="Name..." maxlength="20"
        v-if="isNotSaved" v-model="taskName">
      <h2 class="todo-item-name" v-if="isNotEdited">{{ taskName }}</h2>
      <TodoItemDeleteButton @delete-task="deleteTask" />
    </div>
    <div class="todo-item-body">
      <textarea name="taskText" class="todo-item-text-input" placeholder="description..." rows="10" col="50"
        maxlength="200" v-if="isNotSaved" v-model="taskText"></textarea>
      <p class="todo-item-text" v-if="isNotEdited">{{ taskText }}</p>
    </div>
    <div class="todo-item-footer">
      <input type="date" name="taskDate" class="todo-item-date-input" v-if="isNotSaved" v-model="taskDate">
      <div class="todo-item-date" v-if="isNotEdited">{{ taskDate }}</div>
      <TodoItemEditButton v-if="isNotEdited" @edit-task="editTask" />
      <TodoItemSaveButton v-if="isNotSaved && taskText" @save-task="saveTask" />
    </div>
  </div>
</template>

<style scoped>
.todo-item-container {
  min-width: 17rem;
  max-width: 18rem;
  max-height: 20rem;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  gap: .5rem;
  padding: 1rem;
  border-radius: var(--main-radius);
  background-color: var(--main-color);
  box-shadow: var(--main-shadow);
  border: var(--border-container);
}

.todo-item-top {
  display: flex;
  min-height: 1.7rem;
  align-items: center;
  gap: .5rem;
  border: var(--border-container);
}

.todo-item-name-input {
  display: block;
  flex: 1;
  margin: 0;
  padding: 0;
  font-size: 1rem;
  font-family: 'Courier New', Courier, monospace;
  text-transform: capitalize;
  font-weight: bold;
  letter-spacing: normal;
  word-spacing: normal;
  background-color: var(--main-color);
  color: var(--main-color-text-mod);
  border: var(--border-sub-container);
  color-scheme: dark;
}

.todo-item-name {
  display: flex;
  align-items: center;
  flex: 1;
  margin: 0;
  padding: 0;
  font-size: 1rem;
  font-family: 'Courier New', Courier, monospace;
  text-transform: capitalize;
  font-weight: bold;
  letter-spacing: normal;
  word-spacing: normal;
  background-color: inherit;
  color: inherit;
  border: var(--border-sub-container);
}

button {
  cursor: pointer;
  margin: 0;
  border-radius: var(--main-radius);
  font-size: 1rem;
  padding: .2rem .5rem;
  border: var(--border-button);
  background-color: var(--main-color-lighter);
  color: var(--main-color-text);
  transition: .3s;
}

button:hover {
  background-color: var(--main-color-darker);
  border-color: var(--main-color-darker);
}

button:active {
  background-color: var(--main-color-very-light);
  border-color: var(--main-color-very-light);
  color: var(--main-color-darker);
}

.todo-item-body {
  display: flex;
  border: var(--border-container);
}

.todo-item-text-input {
  display: block;
  width: 100%;
  padding: 0;
  font-size: 1rem;
  letter-spacing: normal;
  word-spacing: normal;
  resize: none;
  background-color: var(--main-color);
  color: var(--main-color-text);
  color-scheme: dark;
  border: var(--border-sub-container);
}

.todo-item-text {
  word-break: break-all;
  white-space: pre-wrap;
  font-size: 1rem;
  letter-spacing: normal;
  word-spacing: normal;
  background-color: inherit;
  color: inherit;
  border: var(--border-sub-container);
}

.todo-item-footer {
  display: flex;
  min-height: 1.7rem;
  flex-flow: row nowrap;
  justify-content: space-between;
  gap: .5rem;
  border: var(--border-container);
}

.todo-item-date-input {
  padding: 0rem .5rem;
  text-transform: uppercase;
  font-family: monospace;
  background-color: var(--main-color-lighter);
  color: var(--main-color-text);
  color-scheme: dark;
  border: var(--border-button);
  border-radius: var(--main-radius);
  transition: .2s;
}

.todo-item-date-input:hover {
  background-color: var(--main-color-darker);
  border-color: var(--main-color-darker);
}

.todo-item-date-input:active {
  background-color: var(--main-color-very-light);
  border-color: var(--main-color-very-light);
}

.todo-item-date {
  display: flex;
  align-items: center;
  background-color: inherit;
  color: inherit;
  border: var(--border-button);
  transition: .2s;
}

.modColor {
  background-color: var(--main-color-mod);
  color: var(--main-color-text-mod);
  box-shadow: var(--main-shadow-mod);

  button {
    background-color: var(--main-color-lighter-mod);
    color: var(--main-color-text-mod);
  }

  button:hover {
    background-color: var(--main-color-darker-mod);
    border-color: var(--main-color-darker-mod);
  }

  button:active {
    background-color: var(--main-color-very-light-mod);
    border-color: var(--main-color-very-light-mod);
    color: var(--main-color-darker-mod);
  }

}
</style>