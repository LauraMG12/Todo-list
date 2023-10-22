<script setup lang="ts">
import TodoList from "@/components/TodoList.vue";
</script>

<template>
  <header>
    <input class="title" type="text" value="Title" />
  </header>
  <main>
    <TodoList />
  </main>
  <footer>
    <p class="copyright">
      @ <span class="highlight">Laura Mañogil González</span> 2023
    </p>
  </footer>
</template>

<style scoped lang="scss">
@import "@/styles/main.scss";
.title {
  all: unset;
  cursor: auto;
  font-size: $font-size-primary-desktop;
  color: $white;
  margin: 25px 0 25px 20px;
  text-overflow: ellipsis;
  @media only screen and (max-width: $medium-breackpoint) {
    font-size: $font-size-primary-mobile;
    margin: 15px 10px;
  }
}
.copyright {
  color: $white;
  margin: 20px;
  text-align: center;

  .highlight {
    color: $primary;
  }
}
</style>
