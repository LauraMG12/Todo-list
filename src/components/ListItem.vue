<script setup lang="ts">
import { ref } from "vue";
import SvgIcon from "./SvgIcon.vue";
interface ListItemProps {
  value: string;
}
interface ListItemEmits {
  (event: "remove"): void;
  (event: "update", value: string): void;
}
const props = defineProps<ListItemProps>();
const emit = defineEmits<ListItemEmits>();

const checked = ref<boolean>(false);
function toggleChecked(): void {
  checked.value = !checked.value;
}
</script>

<template>
  <div class="item-container">
    <div class="check-icon" @click="toggleChecked">
      <SvgIcon v-if="checked" name="checked" />
      <SvgIcon v-else name="unchecked" />
    </div>
    <input
      class="input-field"
      :class="{ checked: checked }"
      type="text"
      :value="props.value"
      @change="emit('update', ($event.target as HTMLInputElement).value)"
    />

    <div class="remove-icon" @click="emit('remove')">
      <SvgIcon name="cross" />
    </div>
  </div>
</template>

<style scoped lang="scss">
@import "@/styles/main.scss";
.item-container {
  background-color: $background-4;
  padding: 10px 20px;
  width: 100%;
  border-radius: 10px;
  display: flex;
  justify-content: space-between;
  gap: 20px;
  align-items: center;
  @media only screen and (max-width: $medium-breackpoint) {
    padding: 8px 10px;
    gap: 10px;
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

  .check-icon,
  .remove-icon {
    height: 25px;
    width: 25px;
    display: flex;
    justify-content: center;
    align-items: center;
    @media only screen and (max-width: $medium-breackpoint) {
      width: 20px;
      height: 20px;
    }
  }
  .check-icon:hover,
  .remove-icon:hover {
    cursor: pointer;
  }
}
</style>
