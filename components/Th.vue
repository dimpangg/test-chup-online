<script setup lang="ts">
import IconSort from "~/assets/icon-sort.svg";
defineProps({
  withSort: Boolean,
});
</script>

<template>
  <th
    class="text-left text-[#1D1D1D] font-medium text-base px-[14px] py-[18px] bg-white first:rounded-tl-lg last:rounded-tr-lg"
  >
    <template v-if="withSort">
      <div class="flex justify-between items-center">
        <slot />
        <IconSort class="text-[#9FA0A1]" />
      </div>
    </template>
    <template v-else>
      <slot />
    </template>
  </th>
</template>
