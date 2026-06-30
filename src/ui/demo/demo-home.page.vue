<script lang="ts" setup>
</script>

<template>
  <div grid grid-cols-5 gap-2>
    <c-button v-for="{ name } of demoRoutes" :key="name" :to="{ name }">
      {{ name }}
    </c-button>
  </div>
</template>
