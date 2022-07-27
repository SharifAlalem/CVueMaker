<template>
  <div>
    <slot></slot>
    <div class="form">
      <BaseInput
        :placeholder="input.placeholder"
        label=""
        :type="input.type"
        :classtype="input.width"
        :disabled="false"
        :formId="id"
        v-for="input in data"
        :key="input.inputName"
        v-model="input[input.inputName]"
      ></BaseInput>
    </div>
  </div>
</template>

<script setup lang="ts">
import BaseInput from "./BaseInput.vue";

import { defineProps } from "vue";

const props = defineProps({
  data: {
    type: Array as any,
    required: true,
  },
  id: {
    type: Number,
    required: false,
    default: null,
  },
});
</script>

<style lang="scss">
.form {
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
  justify-content: center;
  align-items: center;
}

.full {
  width: 100%;
}
</style>
