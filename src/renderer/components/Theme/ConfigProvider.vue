<template>
  <a-config-provider :theme='store.customTheme' :locale="locale">
    <TokenProvider>
      <slot></slot>
    </TokenProvider>
  </a-config-provider>
</template>
<script setup>
import { computed } from 'vue'
import zhCN from 'ant-design-vue/es/locale/zh_CN'
import enUS from 'ant-design-vue/es/locale/en_US'
import frFR from 'ant-design-vue/es/locale/fr_FR'
import TokenProvider from '@/renderer/components/Theme/TokenProvider.vue'
import { useMainStore } from '@/renderer/store'
const store = useMainStore()
const locale = computed(() => {
  const language = store.settings.Language
  if (language === 'zh') {
    return zhCN
  }
  if (language === 'fr') {
    return frFR
  }
  return enUS
})

window.matchMedia('(prefers-color-scheme: dark)').onchange = () => {
  if (store.settings.ThemeMode === 'system') {
    store.changeTheme(store.settings.ThemeMode, store.settings.ThemeColor)
  }
}
</script>

<style>

</style>
