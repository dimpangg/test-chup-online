<script setup lang="ts">
defineProps({
  label: String,
});
</script>

<template>
  <div class="flex flex-col gap-3">
    <Label>{{ label }}</Label>
    <slot />
  </div>
</template>
