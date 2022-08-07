<template>
  <section id="personalInfo">
    <div class="title">
      <h4>Personal Information</h4>
    </div>
    <BaseForm :data="personalInfoData" :withImageUpload="true" />
  </section>
</template>

<script setup lang="ts">
import { defineProps, inject } from "vue";
import BaseForm from "./ui/BaseForm.vue";

const personalInfoData: any = inject("personalInfoData");
</script>
