<script setup>
import UiButton from "./UiButton.vue";
import UiInput from "./UiInput.vue";
import { ref } from "vue";

const emit = defineEmits(['delete-task', 'mod-task'])
const props = defineProps({
  todoItem: Object,
})


const taskId = ref(props.todoItem.id);
const taskName = ref('');
const taskText = ref('');
const taskDate = ref('');
const isSaved = ref(false);

const deleteTask = () => {
  emit('delete-task', taskId.value)
}

const modTask = () => {
  isSaved.value = !isSaved.value
  emit('mod-task', taskId.value, taskName.value, taskText.value, taskDate.value, isSaved.value)
}

</script>

<template>
  <div
    class="todo-item-container"
    :class="{ modColor: isSaved }"
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
        v-if="!isSaved"
      />
      <h2 class="todo-item-name" v-else>{{ taskName }}</h2>
      <UiButton class="task-button" button-type="DELETE" @action="deleteTask">x</UiButton>
    </div>
    <div class="todo-item-body">
      <textarea
        name="taskText"
        class="todo-item-text-input"
        placeholder="description..."
        rows="10"
        maxlength="200"
        v-model="taskText"
        v-if="!isSaved"
      >
      </textarea>
      <p class="todo-item-text" v-else>{{ taskText }}</p>
    </div>
    <div class="todo-item-footer">
      <input
        type="date"
        name="taskDate"
        class="todo-item-date-input"
        v-if="!isSaved"
        v-model="taskDate"
      />
      <div class="todo-item-date" v-else>{{ taskDate }}</div>
      <UiButton class="task-button" v-if="isSaved" @action="modTask">edit</UiButton>
      <UiButton class="task-button" v-if="!isSaved && taskText" @action="modTask">save</UiButton>
    </div>
    <div style="color: red">{{ taskId }}</div>
    <div>{{ todoItem }}</div>
  </div>
</template>

<style scoped>
.todo-item-container {
  min-width: 17rem;
  max-width: 18rem;
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
  padding: 0 0.5rem;
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

  .task-button {
    background-color: var(--main-color-lighter-mod);
    color: var(--main-color-text-mod);
  }

  .task-button:hover {
    background-color: var(--main-color-darker-mod);
    border-color: var(--main-color-darker-mod);
  }

  .task-button:active {
    background-color: var(--main-color-very-light-mod);
    border-color: var(--main-color-very-light-mod);
    color: var(--main-color-darker-mod);
  }
}
</style>
