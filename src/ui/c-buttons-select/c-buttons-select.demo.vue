<script setup lang="ts">
  const _optionsA = [
    { label: 'Option A', value: 'a' },
    { label: 'Option B', value: 'b', tooltip: 'This is a tooltip' },
    { label: 'Option C', value: 'c' },
  ];

  const _optionB = {
    'Option A': 'a',
    'Option B': 'b',
    'Option C': 'c',
  };

  const _valueA = ref('a');
</script>

<template>
  <c-buttons-select v-model:value="valueA" :options="optionsA" label="Label: " />
  <c-buttons-select v-model:value="valueA" :options="optionsA" label="Label: " label-position="left" mt-2 />
  <c-buttons-select v-model:value="valueA" :options="optionB" label="Options object: " />
</template>
