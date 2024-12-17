<template>
  <input :type="type" :name="name" class="todo-item-name-input" :placeholder="placeholder" :maxlength="maxlength"
    :model-value="modelValue" @input="onInput" />
</template>

<script setup>
const props = defineProps({
  modelValue: String,
  type: String,
  name: String,
  placeholder: String,
  maxlength: Number,
});

const emit = defineEmits(["update:model-value"]);

const onInput = (event) => {
  emit("update:model-value", event.target.value);
};
</script>

<style scoped></style>
