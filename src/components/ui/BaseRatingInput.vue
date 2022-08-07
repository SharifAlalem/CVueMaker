<template>
  <div id="rating">
    <ul>
      <li v-for="(rate, index) in maxNum" :key="rate" @click="callback(index)">
        <span v-if="index < value">
          <i class="fa-star star fa-solid"></i>
        </span>
        <span v-else>
          <i class="fa-star star fa-regular"></i>
        </span>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { defineProps, inject } from "vue";

const changeRating: any = inject("changeRating");

const props = defineProps<{
  maxNum: number;
  value: any;
  formId: number;
}>();

const callback = (index: number) => {
  changeRating(index, props.formId);
};
</script>

<style lang="scss" scoped>
#rating {
  display: inline-flex;
  justify-content: center;
  align-items: center;
}
ul {
  list-style: none;
  display: inline-flex;
  padding: 0;
  margin: 0;
}
.star {
  padding: 10px 5px;
  color: #333;
  background-color: #fff;
  border-radius: 4px;
  font-size: 20px;

  &[disabled] {
    cursor: not-allowed;
  }
  &.danger {
    background-color: #ff4949;
    color: #fff;
  }
  &.success {
    background-color: #13ce66;
    color: #fff;
  }
  &.info {
    background-color: #50bfff;
    color: #fff;
  }

  &:hover {
    color: red;
  }
}
</style>
