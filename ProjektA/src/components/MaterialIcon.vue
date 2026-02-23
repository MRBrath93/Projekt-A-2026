<script setup>
import { computed } from "vue";

const props = defineProps({
  name: { type: String, required: true },
  size: { type: String, default: "md" },
});

const sizeClass = computed(() => `icon-${props.size}`);
</script>

<template>
  <span class="material-symbols-rounded" :class="sizeClass" aria-hidden="true">{{ name }}</span>
</template>

<style scoped>
.icon-sm {
  --ms-size: 18px;
  --ms-opsz: 18;
}
.icon-md {
  --ms-size: 24px;
  --ms-opsz: 24;
}
.icon-lg {
  --ms-size: 32px;
  --ms-opsz: 32;
}
</style>