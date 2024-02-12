<script setup lang="ts">
import { cva, type VariantProps } from "class-variance-authority";

defineEmits(['update:modelValue'])

const inputVariants = cva("bg-white placeholder:text-[#9FA0A1] m-0 tex-[#1D1D1D] text-base appearance-none outline-none border border-[#CFD1D4] rounded-md focus:border-[#115934] focus:shadow-[0px_0px_0px_2px_#1159341F] transition-colors duration-200 ease-in-out disabled:border-[#CFD1D4] disabled:text-[#CFD1D4] disabled:placeholder:text-[#CFD1D4] disabled:bg-[#F5F7FA] font-normal", {
  variants: {
    size: {
      large: "px-4 py-[13.5px]",
      medium: "px-3 py-2.5",
      small: "px-[14px] py-[4.5px]",
    },
  },
});

type InputProps = VariantProps<typeof inputVariants>;

withDefaults(defineProps<{ size?: InputProps["size"], modelValue?: string }>(), {
  size: "medium",
  modelValue:""
});
</script>

<template>
  <input
    :class="inputVariants({ size })"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
  />
</template>
