<script setup>
import TodoItemDeleteButton from "./TodoItemDeleteButton.vue";
import TodoItemEditButton from "./TodoItemEditButton.vue";
import TodoItemSaveButton from "./TodoItemSaveButton.vue";
import UiButton from "./UiButton.vue";
import UiInput from "./UiInput.vue";

import { ref } from "vue";
defineProps(["idProp"]);
const taskName = ref();
const taskText = ref();
const taskDate = ref();

const isNotDeleted = ref(true);
const isEdited = ref(true);
const isColorModified = ref(false);

const deleteTask = () => {
  isNotDeleted.value = !isNotDeleted.value;
};

const modTask = () => {
  isEdited.value = !isEdited.value;
  isColorModified.value = !isColorModified.value;
};
</script>

<template>
  <div
    class="todo-item-container"
    v-if="isNotDeleted"
    :class="{ modColor: isColorModified }"
  >
    <div class="todo-item-top">
      <UiInput
        class="todo-item-name-input"
        type="text"
        name="taskTitle"
        placeholder="Name..."
        :maxlength="20"
        :model-value="taskName"
        @update:model-value="taskName = $event"
        v-if="isEdited"
      />
      <h2 class="todo-item-name" v-else>{{ taskName }}</h2>
      <div>{{ idProp }}</div>
      <UiButton @action="deleteTask" buttonType="DELETE">x</UiButton>
    </div>
    <div class="todo-item-body">
      <textarea
        name="taskText"
        class="todo-item-text-input"
        placeholder="description..."
        rows="10"
        col="50"
        maxlength="200"
        v-model="taskText"
        v-if="isEdited"
      >
      </textarea>
      <p class="todo-item-text" v-else>{{ taskText }}</p>
    </div>
    <div class="todo-item-footer">
      <input
        type="date"
        name="taskDate"
        class="todo-item-date-input"
        v-if="isEdited"
        v-model="taskDate"
      />
      <div class="todo-item-date" v-else>{{ taskDate }}</div>
      <TodoItemEditButton v-if="isColorModified" @mod-task="modTask" />
      <TodoItemSaveButton v-if="isEdited && taskText" @mod-task="modTask" />
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
  gap: 0.5rem;
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
  gap: 0.5rem;
  border: var(--border-container);
}

.todo-item-name-input {
  display: block;
  flex: 1;
  margin: 0;
  padding: 0;
  font-size: 1rem;
  font-family: "Courier New", Courier, monospace;
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
  font-family: "Courier New", Courier, monospace;
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
  padding: 0.2rem 0.5rem;
  border: var(--border-button);
  background-color: var(--main-color-lighter);
  color: var(--main-color-text);
  transition: 0.3s;
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
  gap: 0.5rem;
  border: var(--border-container);
}

.todo-item-date-input {
  padding: 0rem 0.5rem;
  text-transform: uppercase;
  font-family: monospace;
  background-color: var(--main-color-lighter);
  color: var(--main-color-text);
  color-scheme: dark;
  border: var(--border-button);
  border-radius: var(--main-radius);
  transition: 0.2s;
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
  color: var(--main-color-very-light-mod);
  border: var(--border-button);
  transition: 0.2s;
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
