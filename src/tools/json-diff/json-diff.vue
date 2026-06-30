<script setup lang="ts">
  import JSON5 from 'json5';
  import { isNotThrowing } from '@/utils/boolean';
  import { withDefaultOnError } from '@/utils/defaults';

  const rawLeftJson = ref('');
  const rawRightJson = ref('');

  const _leftJson = computed(() => withDefaultOnError(() => JSON5.parse(rawLeftJson.value), undefined));
  const _rightJson = computed(() => withDefaultOnError(() => JSON5.parse(rawRightJson.value), undefined));

  const _jsonValidationRules = [
    {
      validator: (value: string) => value === '' || isNotThrowing(() => JSON5.parse(value)),
      message: 'Invalid JSON format',
    },
  ];
</script>

<template>
  <c-input-text
    v-model:value="rawLeftJson"
    :validation-rules="jsonValidationRules"
    label="Your first JSON"
    placeholder="Paste your first JSON here..."
    rows="20"
    multiline
    test-id="leftJson"
    raw-text
    monospace
  />

  <c-input-text
    v-model:value="rawRightJson"
    :validation-rules="jsonValidationRules"
    label="Your JSON to compare"
    placeholder="Paste your JSON to compare here..."
    rows="20"
    multiline
    test-id="rightJson"
    raw-text
    monospace
  />

  <DiffsViewer :left-json="leftJson" :right-json="rightJson" />
</template>
