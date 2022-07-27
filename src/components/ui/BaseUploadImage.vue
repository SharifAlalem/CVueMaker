<template>
  <div class="form-group">
    <div class="form-element">
      <label>
        <img src="@/assets/images/avatar.png" width="100" />
        <input class="file-input" type="file" />
      </label>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineEmits, defineProps } from "vue";

// const props = defineProps<{
//   classtype: string;
//   type: string;
//   label: string;
//   placeholder: string;
//   disabled: boolean;
//   modelValue: any;
// }>();

// const emit = defineEmits<{
//   (e: "update:modelValue", event: Event): void;
// }>();

// const updateValue = (event) => {
//   emit("update:modelValue", event.target.value);
// };
</script>

<style lang="scss" scoped>
.form-group {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.file-input {
  width: 0.1px;
  height: 0.1px;
  opacity: 0;
  overflow: hidden;
  position: absolute;
  z-index: -10;
}

.form-element {
  border-radius: 50%;
  position: relative;
  z-index: 0;

  label {
    border-radius: 50%;
    display: flex;
    align-items: center;
    width: 100%;
    height: 100%;
    font-weight: 400;
    text-overflow: ellipsis;
    white-space: nowrap;
    cursor: pointer;
    overflow: hidden;
    z-index: 0;
    background-color: transparent;

    img {
      z-index: -3;
    }

    &::after {
      content: "+";
      background-color: gray;
      border-radius: 100%;
      border: 1px solid white;
      position: absolute;
      color: white;
      font-size: 25px;
      text-align: center;
      width: 27px;
      height: 26px;
      bottom: -5px;
      left: 36px;
      z-index: -3;
    }
  }
}
</style>
