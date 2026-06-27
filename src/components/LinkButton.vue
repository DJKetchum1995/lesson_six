<script setup lang="ts">
const props = defineProps<{
  label: string
  url: string
  icon?: string
}>()
</script>

<template>
  <v-btn
    :href="url"
    target="_blank"
    rel="noreferrer noopener"
    variant="tonal"
    block
    size="large"
    class="link-button"
  >
    <v-icon v-if="icon" left>{{ icon }}</v-icon>
    {{ label }}
  </v-btn>
</template>

<style scoped>
.link-button {
  border: 1.5px solid rgba(29, 233, 182, 0.95);
  border-radius: 36px;
}
</style>
