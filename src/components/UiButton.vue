<script setup>
import { computed } from "vue";

const emit = defineEmits(["action"]);
const props = defineProps({
  buttonType: String,
});

const isItDeleteButton = computed(() => props.buttonType === "DELETE");
const onClick = () => {
  emit("action");
  // console.log("GAVNO");
};
</script>

<template>
  <button @click="onClick" type="button" :class="{ red: isItDeleteButton }">
    <slot />
  </button>
</template>

<style scoped>
.block {
  display: block;
}

.red {
  background: red;
  color: white;
}
</style>
