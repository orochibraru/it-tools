<script setup lang="ts">
  import { parse as parseToml } from 'iarna-toml-esm';
  import type { UseValidationRule } from '@/composable/validation';
  import { withDefaultOnError } from '../../utils/defaults';
  import { isValidToml } from './toml.services';

  const _transformer = (value: string) =>
    value === '' ? '' : withDefaultOnError(() => JSON.stringify(parseToml(value), null, 3), '');

  const _rules: UseValidationRule<string>[] = [
    {
      validator: isValidToml,
      message: 'Provided TOML is not valid.',
    },
  ];
</script>

<template>
  <format-transformer
    input-label="Your TOML"
    input-placeholder="Paste your TOML here..."
    output-label="JSON from your TOML"
    output-language="json"
    :input-validation-rules="rules"
    :transformer="transformer"
  />
</template>
