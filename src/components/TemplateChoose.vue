<template>
  <section id="template">
    <div class="title">
      <h4>Templates</h4>
    </div>
    <div class="templates">
      <router-link
        class="templateImage"
        :to="`template_${template.templateId}`"
        v-for="template in templatesInfoData"
        :key="template.templateId"
      >
        <img src="@/assets/images/avatar.png" alt="template" width="100" />
      </router-link>
    </div>
  </section>
</template>
<script setup lang="ts">
import { inject } from "vue";

const templatesInfoData: any = inject("templatesInfoData");
</script>

<style lang="scss" scoped>
.templates {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
  padding: 20px;

  .templateImage {
    width: 28%;
    border: 1px solid gray;
    border-radius: 10px;
    margin: 5px;
    cursor: pointer;
  }
}
</style>
