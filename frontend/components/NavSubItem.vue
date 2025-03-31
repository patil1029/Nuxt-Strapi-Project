<template>
  <NuxtLink class="nav" :to="url || ''">{{ name }}</NuxtLink>
</template>

<script lang="ts" setup>
const props = defineProps({
  name: {
    type: String as PropType<string | null | undefined>,
  },
  url: {
    type: String as PropType<string | null | undefined>,
  },
});
</script>
