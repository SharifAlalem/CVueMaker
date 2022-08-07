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
  border: none;
  text-transform: uppercase;
  color: #333;
  background-color: #fff;
  border-radius: 4px;
  font-size: 14px;
  transition: all 0.2s;
  cursor: pointer;
  &[disabled] {
    cursor: not-allowed;
  }
  &.danger {
    background-color: $red;
    color: #fff;

    &:hover {
      box-shadow: $shadow;
      border: 2px solid $dark-red;
      color: $dark-red;
    }
  }
  &.success {
    background-color: $green;
    color: #fff;

    &:hover {
      box-shadow: $shadow;
      border: 2px solid $dark-green;
      color: $dark-green;
    }
  }
  &.info {
    background-color: $blue;
    color: #fff;
  }

  &.transparent {
    background-color: transparent;
    border: 1px solid black;
    border-radius: 0;

    &:hover {
      box-shadow: $shadow;
      background-color: white;
    }
  }
}
</style>
