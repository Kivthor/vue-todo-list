<template>
  <input 
  class="todo-item-name-input" 
  :type="type" 
  :name="name" 
  :placeholder="placeholder" 
  :maxlength="maxlength"
  :model-value="modelValue" 
  @input="onInput" 
  />
</template>

<script setup>
const props = defineProps({
  type: String,
  name: String,
  placeholder: String,
  maxlength: Number,
  modelValue: String,
});

const emit = defineEmits(["update:model-value"]);

const onInput = (event) => {
  emit("update:model-value", event.target.value);
};
</script>

<style scoped></style>
