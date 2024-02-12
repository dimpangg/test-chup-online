<script setup lang="ts">
import { cva, type VariantProps } from "class-variance-authority";

const button = cva("transition-colors duration-200 ease-in-out border", {
  variants: {
    intent: {
      primary: "bg-[#115934] text-white hover:bg-[#87D5AD] active:bg-[#0A331E] border-transparent disabled:border-[#CFD1D4] disabled:bg-[#EBEDF0] disabled:text-[#CFD1D4]",
      secondary: "bg-[#F26522] text-white hover:bg-[#F7A178] active:bg-[#9A3809] border-transparent disabled:border-[#CFD1D4] disabled:bg-[#EBEDF0] disabled:text-[#CFD1D4]",
      tertiary: "bg-white text-[#1D1D1D] hover:bg-[#F5F7FA] active:bg-[#CFD1D4] border-[#CFD1D4] disabled:border-[#CFD1D4] disabled:bg-[#EBEDF0] disabled:text-[#CFD1D4]",
      dashed: "bg-white text-[#1D1D1D] hover:border-[#87D5AD] hover:text-[#87D5AD] active:border-[#0A331E] active:text-[#0A331E] border-[#CFD1D4] border-dashed disabled:border-[#CFD1D4] disabled:border-dashed disabled:bg-[#EBEDF0] disabled:text-[#CFD1D4]",
      link: "underline text-[#115934] hover:text-[#87D5AD] active:text-[#0A331E] disabled:text-[#BDBEBF] border-0",
      text: "bg-white text-[#1D1D1D] hover:bg-[#F5F7FA] active:bg-[#EBEDF0] border-transparent disabled:bg-white disabled:text-[#BDBEBF]",
    },
    size: {
      small: "px-2.5 py-2 text-sm/[17px] rounded-md",
      medium: "py-3 px-4 text-base/5 rounded-lg",
      large:"py-[14px] px-5 text-[18px]/[23px] rounded-lg"
    },
  },
});

type ButtonProps = VariantProps<typeof button>;

withDefaults(
  defineProps<{ intent?: ButtonProps["intent"]; size?: ButtonProps["size"] }>(),
  {
    intent: "primary",
    size: "medium",
  },
);
</script>

<template>
  <button :class="button({ intent, size })">
    <slot />
  </button>
</template>
