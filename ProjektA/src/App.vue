<script setup>
import { ref, computed, watch, onMounted } from "vue";
import TextInput from "./components/TextInput.vue";
import StatsTable from "./components/StatsTable.vue";
import BaseButton from "./components/BaseButton.vue";
import ToggleSwitch from "./components/ToggleSwitch.vue";
import MaterialIcon from "./components/MaterialIcon.vue";

const text = ref("");
const showStats = ref(true);
const isDark = ref(false);

const stats = computed(() => {
  const t = text.value;

  const charCount = t.length;
  // \s matcher alle whitespace-tegn, \S matcher alle ikke-whitespace.
  const whitespaceCount = (t.match(/\s/g) || []).length;
  const nonWhitespaceCount = (t.match(/\S/g) || []).length;

  // Unicode regex for uppercase (Lu) og lowercase (Ll). Bruges i stedet for [A-Z] og [a-z] for at understøtte alle sprog.
  const uppercaseCount = (t.match(/\p{Lu}/gu) || []).length;
  const lowercaseCount = (t.match(/\p{Ll}/gu) || []).length;

  // Split på whitespace for at få ord.
  const words = t.trim() ? t.trim().split(/\s+/) : [];
  const wordCount = words.length;

  // Split på ., !, ? for at få sætninger. Trim og filter for at undgå tomme sætninger. Boolean i filter fjerner falsy værdier som tomme strenge.
  const sentenceCount = t.trim()
    ? t.trim().split(/[.!?]+/).map(s => s.trim()).filter(Boolean).length
    : 0;

  const avgWordLength =
    wordCount === 0 ? 0 : words.reduce((sum, w) => sum + w.length, 0) / wordCount;

  return {
    charCount,
    wordCount,
    sentenceCount,
    avgWordLength,
    whitespaceCount,
    nonWhitespaceCount,
    uppercaseCount,
    lowercaseCount,
  };
});

function clearText() {
  text.value = "";
}

function makeUppercase() {
  text.value = text.value.toUpperCase();
}

function makeLowercase() {
  text.value = text.value.toLowerCase();
}

function toggleTheme() {
  isDark.value = !isDark.value;
}

function applyTheme() {
  const root = document.documentElement;
  root.classList.toggle("theme-dark", isDark.value);
  root.classList.toggle("theme-light", !isDark.value);
}

onMounted(() => {
  // Start ud fra systemets theme
  isDark.value = window.matchMedia("(prefers-color-scheme: dark)").matches;
  applyTheme();
});

watch(isDark, applyTheme);
</script>

<template>
  <div class="wrap">
    <div>
      <h1>
        Teksanalysator & editor
        <MaterialIcon name="bar_chart" size="lg" />
      </h1>

      <TextInput v-model="text" />

      <div class="buttons">
        <BaseButton variant="primary" @click="makeUppercase">Store bogstaver</BaseButton>
        <BaseButton variant="secondary" @click="makeLowercase">Små bogstaver</BaseButton>
        <BaseButton variant="danger" @click="clearText">Ryd tekst</BaseButton>
      </div>
      <div class="buttons">
        <ToggleSwitch v-model="showStats" label="Vis statistik" />
      </div>
      <div class="buttons">
        <ToggleSwitch v-model="isDark" label="Dark mode" />
      </div>
    </div>

    <Transition name="fade">
      <StatsTable v-if="showStats" :stats="stats" />
    </Transition>
  </div>
</template>

<style scoped>
.wrap { 
  max-width: 1200px; 
  margin: 24px auto; 
  padding: 0 12px; 
}

h1{
  display: flex;
  align-items: center;
  gap: 8px;
}

.buttons{
  display: flex;
  gap: 1rem;
  margin: 12px 0;
}
</style>