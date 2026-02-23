<script setup>
// Komponenten implementerer v-model ved at modtage værdien som en prop (modelValue) og sende ændringer tilbage til parent via et update:modelValue-event.
defineProps({ modelValue: { type: String, default: "" } });
defineEmits(["update:modelValue"]);
</script>

<template>
  <textarea
    class="input"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    rows="8"
    placeholder="Skriv din tekst her..."
  />
</template>

<style scoped>
.input { 
    width: 100%; 
    padding: 10px; 
    font-size: 16px; 
    border: 1px solid #ccc; 
    border-radius: 10px; 
    font-family: "Poppins", sans-serif; }
</style>