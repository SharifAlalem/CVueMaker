<template>
  <div id="home">
    <BaseCard @prevComp="back" @nextComp="after" :currentIndex="currentIndex">
      <keep-alive>
        <transition name="fade" mode="out-in">
          <component class="component" :is="components[currentIndex].compName"></component>
        </transition>
      </keep-alive>
    </BaseCard>
  </div>
</template>

<script setup lang="ts">
import PersonalInfo from "@/components/PersonalInfo.vue";
import EducationInfo from "@/components/EducationInfo.vue";
import WorkInfo from "@/components/WorkInfo.vue";
import ProjectsInfo from "@/components/ProjectsInfo.vue";
import SkillsInfo from "@/components/SkillsInfo.vue";
import TemplateChoose from "@/components/TemplateChoose.vue";
import BaseCard from "@/components/ui/BaseCard.vue";
import { shallowRef, inject, watch } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();
// fetch the user information when params change
watch(
  () => route,
  async (newId) => {
    console.log(route);
  }
);

let currentIndex = shallowRef(0);

const updateFormsData: any = inject("updateFormsData");
const removeFormsData: any = inject("removeFormsData");

let components = shallowRef([
  { compName: PersonalInfo },
  { compName: EducationInfo },
  { compName: WorkInfo },
  { compName: ProjectsInfo },
  { compName: SkillsInfo },
  { compName: TemplateChoose },
]);

const back = () => {
  currentIndex.value--;
};

const after = () => {
  currentIndex.value !== components.value.length - 1 ? currentIndex.value++ : "";
};
</script>

<style lang="scss">
#home {
  padding: 150px 0;
  min-height: 100vh;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
