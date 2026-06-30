<script setup lang="ts">
  import JSON5 from 'json5';
  import type { UseValidationRule } from '@/composable/validation';
  import { withDefaultOnError } from '@/utils/defaults';

  const _defaultValue = '{\n\t"hello": [\n\t\t"world"\n\t]\n}';
  const _transformer = (value: string) => withDefaultOnError(() => JSON.stringify(JSON5.parse(value), null, 0), '');

  const _rules: UseValidationRule<string>[] = [
    {
      validator: (v: string) => v === '' || JSON5.parse(v),
      message: 'Provided JSON is not valid.',
    },
  ];
</script>

<template>
  <format-transformer
    input-label="Your raw JSON"
    :input-default="defaultValue"
    input-placeholder="Paste your raw JSON here..."
    output-label="Minified version of your JSON"
    output-language="json"
    :input-validation-rules="rules"
    :transformer="transformer"
  />
</template>
