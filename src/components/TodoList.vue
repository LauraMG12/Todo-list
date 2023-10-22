<script setup lang="ts">
import { ref } from "vue";

import ListItem from "./ListItem.vue";
import NewItem from "./NewItem.vue";

interface todoItem {
  id: string;
  content: string;
}
const items = ref<todoItem[]>([
  { id: crypto.randomUUID().toString(), content: "Hello" },
  { id: crypto.randomUUID().toString(), content: "world!" },
]);

function addItem(inputText: string): void {
  const newItem: todoItem = {
    id: crypto.randomUUID().toString(),
    content: inputText,
  };
  items.value.push(newItem);
}
function removeItem(itemId: string): void {
  const index = items.value.findIndex((item) => item.id === itemId);
  items.value.splice(index, 1);
}
function updateItem(itemId: string, newValue: string): void {
  const index = items.value.findIndex((item) => item.id === itemId);
  items.value[index].content = newValue;
}
</script>

<template>
  <div class="todo-list">
    <TransitionGroup name="list" tag="div" class="items-list">
      <ListItem
        v-for="item in items"
        :key="item.id"
        :value="item.content"
        class="list-item"
        @remove="removeItem(item.id)"
        @update="updateItem(item.id, $event)"
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
  position: relative;
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
    display: block;
    padding: 0 5px;
    max-height: calc(
      100vh -
        (
          $title-height + $footer-height + $add-item-height +
            $todo-container-margin-height + $add-item-list-gap
        )
    );
    overflow-y: scroll;
    overflow-x: hidden;
    position: relative;
    @media only screen and (max-width: $medium-breackpoint) {
      gap: 10px;
      max-height: calc(
        100vh -
          (
            $title-height-mobile + $footer-height-mobile +
              $add-item-height-mobile + $todo-container-margin-height-mobile +
              $add-item-list-gap-mobile
          )
      );
    }
    .list-item:not(:last-child) {
      margin-bottom: 15px;
      @media only screen and (max-width: $medium-breackpoint) {
        margin-bottom: 10px;
      }
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
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: scaleY(0.01) translate(30px, 0);
}
.list-leave-active {
  position: absolute;
}
</style>
