<script setup lang="ts">
  import { darkTheme } from 'naive-ui';
  import { useRoute } from 'vue-router';
  import { layouts } from './layouts';
  import { useStyleStore } from './stores/style.store';
  import { darkThemeOverrides, lightThemeOverrides } from './themes';

  const route = useRoute();
  const _layout = computed(() => route?.meta?.layout ?? layouts.base);
  const styleStore = useStyleStore();

  const _theme = computed(() => (styleStore.isDarkTheme ? darkTheme : null));
  const _themeOverrides = computed(() => (styleStore.isDarkTheme ? darkThemeOverrides : lightThemeOverrides));

  const { locale } = useI18n();

  syncRef(locale, useStorage('locale', locale));
</script>

<template>
  <n-config-provider :theme="theme" :theme-overrides="themeOverrides">
    <NGlobalStyle />
    <NMessageProvider placement="bottom">
      <NNotificationProvider placement="bottom-right">
        <component :is="layout">
          <RouterView />
        </component>
      </NNotificationProvider>
    </NMessageProvider>
  </n-config-provider>
</template>

<style>
body {
  min-height: 100%;
  margin: 0;
  padding: 0;
}

html {
  height: 100%;
  margin: 0;
  padding: 0;
}

* {
  box-sizing: border-box;
}
</style>
