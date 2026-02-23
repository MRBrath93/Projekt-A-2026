<template>
  <label class="switch">
    <input
      type="checkbox"
      :checked="modelValue"
      @change="$emit('update:modelValue', $event.target.checked)"
    />

    <span class="slider"></span>

    <span v-if="label" class="text">{{ label }}</span>
  </label>
</template>

<script setup>
defineProps({
  modelValue: { type: Boolean, default: false },
  label: { type: String, default: "" },
});
defineEmits(["update:modelValue"]);
</script>

<style scoped>
.switch {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  user-select: none;
}

/* Skjul checkbox men behold funktionalitet */
.switch input {
  position: absolute;
  opacity: 0;
  width: 0;
  height: 0;
}

/* Track (baggrund) */
.slider {
  width: 48px;
  height: 28px;
  background: #ffffff;
  border-radius: 999px;
  position: relative;
  transition: background 200ms ease;
}

/* Knop */
.slider::before {
  content: "";
  width: 22px;
  height: 22px;
  position: absolute;
  top: 3px;
  left: 3px;
  background: var(--color-button-primary-bg);
  border-radius: 999px;
  transition: transform 200ms ease;
}

/* Når checked → skift farve + flyt knop */
.switch input:checked + .slider {
  background: var(--color-toggle-bg);
}

.switch input:checked + .slider::before {
  transform: translateX(20px);
}

.text {
  font-size: 14px;
}

</style>