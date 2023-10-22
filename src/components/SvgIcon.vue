<script setup lang="ts">
import { computed, defineAsyncComponent } from "vue";

interface SvgIconProps {
  name: string;
}

const props = defineProps<SvgIconProps>();

const iconPath = computed(() =>
  defineAsyncComponent(() => import(`../assets/${props.name}.svg`))
);
</script>

<template>
  <Suspense>
    <component :is="iconPath" :class="props.name" />
  </Suspense>
</template>
