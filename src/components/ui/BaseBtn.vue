<template>
  <button class="normal" :class="type" :disabled="disabled" @click="callback($event)">
    <slot></slot>
  </button>
</template>

<script setup lang="ts">
import { defineEmits, defineProps } from "vue";

const props = defineProps<{
  type: string;
  disabled: boolean;
}>();

const emit = defineEmits<{
  (e: "click"): void;
}>();

const callback = (e: any) => {
  emit("click");
};
</script>

<style lang="scss" scoped>
button {
  padding: 10px 20px;
  border: 2px solid white;
  text-transform: uppercase;
  color: #333;
  background-color: #fff;
  border-radius: 4px;
  font-size: 14px;
  box-shadow: 0px 3px 4px 0.01px rgba(0, 0, 0, 0.4);
  cursor: pointer;
  &[disabled] {
    cursor: not-allowed;
  }
  &.danger {
    background-color: $red;
    color: #fff;
  }
  &.success {
    background-color: $green;
    color: #fff;
  }
  &.info {
    background-color: $blue;
    color: #fff;
  }
}
</style>
