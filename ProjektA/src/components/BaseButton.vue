<script setup>
defineProps({
  variant: {
    type: String,
    default: "primary",
  },
  type: {
    type: String,
    default: "button",
  },
});

defineEmits(["click"]);
</script>

<template>
  <button
    class="btn"
    :class="`btn--${variant}`"
    :type="type"
    @click="$emit('click')"
  >
    <slot />
  </button>
</template>

<style scoped>
.btn {
  padding: 10px 16px;
  border-radius: 10px;
  border: none;
  cursor: pointer;
}

/* Forskellige varianter */
.btn--primary {
    background: var(--color-button-primary-bg);
    color: var(--color-button-text);
    border: 1px solid var(--color-button-primary-border);
}
.btn--primary:hover {
    background: var(--color-button-primary-bg-hover);
}



.btn--secondary {
    background: var(--color-button-secondary-bg);
    color: var(--color-text);
    border: 1px solid var(--color-button-secondary-border);
}
.btn--secondary:hover {
    background: var(--color-button-secondary-bg-hover);
}



.btn--danger {
    background: var(--color-button-danger-bg);
    color: var(--color-button-text);
    border: 1px solid var(--color-button-danger-border);
}
.btn--danger:hover {
    background: var(--color-button-danger-bg-hover);
}
</style>