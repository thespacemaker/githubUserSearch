<script setup lang="ts">
// https://github.com/vueuse/head
// you can use this to manipulate the document head in any components,
// they will be rendered correctly in the html results with vite-ssg
useHead({
  title: 'Github Searcher',
  meta: [
    { name: 'description', content: 'Github search app made by Spacemaker' },
    {
      name: 'theme-color',
      content: computed(() => isDark.value ? '#00aba9' : '#ffffff'),
    },
  ],
  link: [
    {
      rel: 'icon',
      type: 'image/svg+xml',
      href: computed(() => preferredDark.value ? '/favicon-dark.svg' : '/favicon.svg'),
    },
  ],
})
</script>

<template>
  <RouterView />
  <p class="text-xs text-center">
    Made with &#9825; by <a
      href="https://adnan.io" target="_blank"
    >Spacemaker</a>
  </p>
</template>
