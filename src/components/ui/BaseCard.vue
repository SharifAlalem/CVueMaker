<template>
  <section id="baseCard">
    <slot></slot>
    <div class="actions">
      <BaseBtn v-if="props.currentIndex !== 0" type="danger" :disabled="false" @click="prev"
        >Prev</BaseBtn
      >
      <BaseBtn v-if="props.currentIndex !== 5" type="success" :disabled="false" @click="next"
        >Next</BaseBtn
      >
    </div>
  </section>
</template>

<script setup lang="ts">
import BaseBtn from "./BaseBtn.vue";
import { defineEmits, defineProps } from "vue";

const props = defineProps<{
  currentIndex: any;
}>();
const emit = defineEmits<{
  (e: "prevComp"): void;
  (e: "nextComp"): void;
}>();

const prev = () => {
  emit("prevComp");
};

const next = () => {
  emit("nextComp");
};
</script>

<style lang="scss">
#baseCard {
  background-color: white;
  border-radius: 10px;
  box-shadow: 0 15px 20px rgba(0, 0, 0, 0.5);
  width: 50%;
  padding: 30px;
}

.actions {
  width: 100%;
  display: inline-flex;
  justify-content: space-between;
}
</style>
