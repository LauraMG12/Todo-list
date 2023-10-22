<script setup lang="ts">
interface AddButtonProps {
  disabled: boolean;
}
interface AddButtonEmits {
  (event: "add-item"): void;
}
defineProps<AddButtonProps>();
const emit = defineEmits<AddButtonEmits>();
</script>

<template>
  <button
    :disabled="disabled"
    class="button-container"
    :class="{ disabled: disabled }"
    @click="emit('add-item')"
  >
    <p class="button-text">Add</p>
  </button>
</template>

<style scoped lang="scss">
@import "@/styles/main.scss";

button {
  all: unset;
  transition: all $transition-1;
}
.button-container {
  padding: 8px 20px;
  background-color: $primary;
  color: $white;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  &:disabled {
    background-color: $grey;
    color: $background-1;
    &:hover {
      cursor: default;
    }
  }
  &:hover {
    cursor: pointer;
  }
  .button-text {
    font-weight: 600;
    user-select: none;
  }
}
</style>
