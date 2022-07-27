<template>
  <div class="form-group" :class="type !== 'image' ? classtype : 'block'">
    <div class="label" v-if="label !== ''">
      <p>{{ label }}</p>
    </div>
    <div class="form-element">
      <BaseUploadImage v-if="type === 'image'" class="block"></BaseUploadImage>
      <BaseRatingInput
        v-else-if="type === 'rating'"
        :maxNum="5"
        :formId="formId"
        class="block"
        :value="modelValue"
      ></BaseRatingInput>

      <input
        v-else-if="type !== 'textarea'"
        class="full"
        :type="type"
        :disabled="disabled"
        :placeholder="placeholder"
        :value="modelValue"
        @input="updateValue"
      />
      <textarea
        v-else
        :type="type"
        class="full"
        :disabled="disabled"
        :placeholder="placeholder"
        :value="String(modelValue)"
        @input="updateValue"
      ></textarea>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineEmits, defineProps } from "vue";
import BaseUploadImage from "./BaseUploadImage.vue";
import BaseRatingInput from "./BaseRatingInput.vue";

const props = defineProps({
  classtype: {
    type: String,
    required: true,
  },
  type: {
    type: String,
    required: false,
    default: null,
  },
  label: {
    type: String,
    required: false,
    default: null,
  },
  placeholder: {
    type: String,
    required: false,
    default: null,
  },
  disabled: {
    type: Boolean,
    required: false,
    default: null,
  },
  modelValue: {
    required: false,
    validator: (v) => true,
    default: null,
  },
  formId: {
    type: Number,
    required: false,
    default: null,
  },
});

const emit = defineEmits<{
  (e: "update:modelValue", event: Event): void;
}>();

const updateValue = (event: any) => {
  emit("update:modelValue", event.target.value);
};
</script>

<style lang="scss" scoped>
$breakpoint-tablet: 860px;

.form-group {
  margin: 10px 2%;
}
input,
textarea {
  padding: 10px 5px;
  border: 2px solid #ddd;
  color: #333;
  background-color: #fff;
  border-radius: 4px;
  font-size: 14px;
  resize: none;
  &[disabled] {
    cursor: not-allowed;
  }
  &.danger {
    border-color: #ff4949;
  }
  &.success {
    border-color: #13ce66;
  }
  &.info {
    border-color: #50bfff;
  }
}

.small {
  width: 29.3%;

  @media (max-width: $breakpoint-tablet) {
    width: 100%;
  }
}

.medium {
  width: 44%;
}

.full {
  width: 95%;
}

.block {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
