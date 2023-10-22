<script setup lang="ts">
import { ref, watch } from "vue";

import ListItem from "./ListItem.vue";
import NewItem from "./NewItem.vue";

const items = ref<string[]>(["Hello", "world!"]);
watch(items, () => console.log(items.value));

function addItem(inputText: string): void {
  items.value.push(inputText);
}
function removeItem(index: number): void {
  items.value.splice(index, 1);
}
function updateItem(index: number, newValue: string): void {
  items.value.splice(index, 1, newValue);
}

//TODO: update item
</script>

<template>
  <div class="todo-list">
    <TransitionGroup
      name="listItem"
      tag="div"
      class="items-list"
      ref="itemsList"
    >
      <ListItem
        v-for="(item, index) in items"
        :key="item"
        :value="item"
        @remove="removeItem(index)"
        @update="updateItem(index, $event)"
      />
    </TransitionGroup>
    <div class="add-item">
      <NewItem @add-item="addItem" />
    </div>
  </div>
</template>

<style scoped lang="scss">
@import "@/styles/main.scss";

.todo-list {
  background-color: $background-2;
  border-radius: 15px;
  padding: 25px 10px;
  display: grid;
  min-height: 100%;
  grid-template-rows: 1fr auto;
  width: $medium-breackpoint;
  @media only screen and (max-width: $medium-breackpoint) {
    background-color: transparent;
    margin: 0;
    padding: 0 5px 0 10px;
    width: 100vw;
    height: calc(100% - 30px);
  }

  .items-list {
    display: flex;
    flex-direction: column;
    gap: 15px;
    // FIXME: fixed height to keep when scroll bar appears
    max-height: 90%;
    overflow-y: scroll;
    position: relative;
    @media only screen and (max-width: $medium-breackpoint) {
      gap: 10px;
      height: calc(100% - 80px);
    }
  }
  .add-item {
    display: flex;
    align-items: flex-end;
    @media only screen and (max-width: $medium-breackpoint) {
      background-color: $background-2;
      position: absolute;
      bottom: 0;
      left: 0;
      width: 100vw;
      align-items: center;
    }
  }
}
</style>
