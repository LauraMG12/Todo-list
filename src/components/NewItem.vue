<script setup lang="ts">
import AddButton from "./AddButton.vue";
import { ref } from "vue";

interface AddButtonEmits {
  (event: "add-item", value: string): void;
}
const emit = defineEmits<AddButtonEmits>();
const itemText = ref<string>("");

function addItem(): void {
  if (itemText.value === "") {
    return;
  }
  emit("add-item", itemText.value);
  itemText.value = "";
}
</script>

<template>
  <div class="item-container">
    <input
      class="input-field"
      type="text"
      placeholder="Type here"
      v-model="itemText"
      @keydown.enter="addItem"
    />
    <AddButton :disabled="itemText === ''" @add-item="addItem" />
  </div>
</template>

<style scoped lang="scss">
@import "@/styles/main.scss";

.item-container {
  background-color: $background-4;
  padding: 10px 10px 10px 20px;
  width: 100%;
  border-radius: 10px;
  display: flex;
  justify-content: space-between;
  gap: 20px;
  align-items: center;

  @media only screen and (max-width: $medium-breackpoint) {
    padding: 10px 10px;
    gap: 10px;
    background-color: transparent;
  }
  @media only screen and (min-width: $medium-breackpoint) {
    height: 45px;
  }
  .input-field {
    width: 100%;
    font-size: $font-size-secondary-desktop;
    color: $white;
    background-color: transparent;
    border: none;
    &.checked {
      color: $grey;
      text-decoration: line-through;
    }
    &:focus {
      outline: none;
    }
    @media only screen and (max-width: $medium-breackpoint) {
      font-size: $font-size-secondary-mobile;
    }
  }
}
</style>
