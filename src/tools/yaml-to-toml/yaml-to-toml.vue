<script setup lang="ts">
  import { stringify as stringifyToml } from 'iarna-toml-esm';
  import { parse as parseYaml } from 'yaml';
  import type { UseValidationRule } from '@/composable/validation';
  import { withDefaultOnError } from '../../utils/defaults';

  const convertYamlToToml = (value: string) => [stringifyToml(parseYaml(value))].flat().join('\n').trim();

  const _transformer = (value: string) =>
    value.trim() === '' ? '' : withDefaultOnError(() => convertYamlToToml(value), '');

  const _rules: UseValidationRule<string>[] = [
    {
      validator: (v: string) => v === '' || parseYaml(v),
      message: 'Provided JSON is not valid.',
    },
  ];
</script>

<template>
  <format-transformer
    input-label="Your YAML"
    input-placeholder="Paste your YAML here..."
    output-label="TOML from your YAML"
    output-language="toml"
    :input-validation-rules="rules"
    :transformer="transformer"
  />
</template>
