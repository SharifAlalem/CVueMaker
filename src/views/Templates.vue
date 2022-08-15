<template>
  <div id="templates">
    <keep-alive>
      <transition name="fade" mode="out-in">
        <BaseTemplateCard>
          <component class="component" :is="template_1"></component>
        </BaseTemplateCard>
      </transition>
    </keep-alive>
  </div>
</template>
<script setup lang="ts">
import BaseTemplateCard from "@/components/ui/BaseTemplateCard.vue";
import template_1 from "@/components/templates/template_1.vue";
</script>

<style lang="scss" scoped>
#templates {
  padding: 100px 80px;
  height: 100%;

  @media (max-width: $breakpoint-mobile) {
    padding: 100px 20px;
  }
}
</style>
