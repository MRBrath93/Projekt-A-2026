<template>
  <table class="stats">
    <thead>
      <tr><th>Statistik</th><th>Værdi</th></tr>
    </thead>
    <tbody>
      <tr><td>Karakterer</td><td class="value">{{ stats.charCount }}</td></tr>
      <tr><td>Ord</td><td>{{ stats.wordCount }}</td></tr>
      <tr><td>Sætninger</td><td>{{ stats.sentenceCount }}</td></tr>
      <tr><td>Gns. ordlængde</td><td>{{ stats.avgWordLength.toFixed(2) }}</td></tr>
      <tr><td>Whitespaces</td><td>{{ stats.whitespaceCount }}</td></tr>
      <tr><td>Skrifttegn (ikke-whitespace)</td><td>{{ stats.nonWhitespaceCount }}</td></tr>
      <tr><td>Store bogstaver</td><td>{{ stats.uppercaseCount }}</td></tr>
      <tr><td>Små bogstaver</td><td>{{ stats.lowercaseCount }}</td></tr>
    </tbody>
  </table>
</template>

<script setup>
defineProps({ 
    stats: { 
        type: Object, 
        required: true 
    } 
});
</script>

<style scoped>
.stats { 
    width: 100%; 
    border-collapse: collapse; 
    margin-top: 1rem;
    border-radius: 10px;
    overflow: hidden;

}
.stats th, .stats td { 
    padding: 10px; 
    text-align: left; 
}
tr:nth-child(even), tr:nth-child(0n) {
    background-color: var(--color-button-primary-bg);
    border-radius: 16px;
    color: var(--color-button-text);
}

thead tr {
    background-color: var(--color-button-primary-bg);
    border-radius: 16px;
    color: var(--color-button-text);
}

th{
        font-weight: bold;
        text-transform: uppercase;
}

</style>