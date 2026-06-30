<script setup lang="ts">
  import JSON5 from 'json5';
  import { stringify } from 'yaml';
  import type { UseValidationRule } from '@/composable/validation';
  import { isNotThrowing } from '@/utils/boolean';
  import { withDefaultOnError } from '@/utils/defaults';

  const _transformer = (value: string) => withDefaultOnError(() => stringify(JSON5.parse(value)), '');

  const _rules: UseValidationRule<string>[] = [
    {
      validator: (value: string) => value === '' || isNotThrowing(() => stringify(JSON5.parse(value))),
      message: 'Provided JSON is not valid.',
    },
  ];
</script>

<template>
  <format-transformer
    input-label="Your JSON"
    input-placeholder="Paste your JSON here..."
    output-label="YAML from your JSON"
    output-language="yaml"
    :input-validation-rules="rules"
    :transformer="transformer"
  />
</template>
