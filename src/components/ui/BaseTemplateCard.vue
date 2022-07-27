<template>
  <div id="templateCard" :style="bgColor">
    <Vue3Html2pdf
      :show-layout="true"
      :float-layout="false"
      :enable-download="true"
      :preview-modal="true"
      :paginate-elements-by-height="1400"
      filename="myPDF"
      :pdf-quality="5"
      :manual-pagination="false"
      pdf-format="a4"
      pdf-orientation="portrait"
      pdf-content-width="100%"
      ref="html2Pdf"
    >
      <template #pdf-content>
        <slot></slot>
      </template>
    </Vue3Html2pdf>
    <div class="actions">
      <input type="color" :value="bgColor['--bg-color']" @change="changebgColor" />
      <input type="color" :value="bgColor['--font-color']" @change="changefontColor" />
      <button @click="generateReport">Generate</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import Vue3Html2pdf from "vue3-html2pdf";
import { ref, reactive, provide } from "vue";

let bgColor = reactive({ "--bg-color": "#0930A5", "--font-color": "#ffffff" });
provide("bgColor", bgColor);
const changebgColor = ($event: any) => {
  console.log($event);
  bgColor["--bg-color"] = $event.target.value;
};

const changefontColor = ($event: any) => {
  console.log($event);
  bgColor["--font-color"] = $event.target.value;
};

let html2Pdf: any = ref(null);
const generateReport = () => {
  html2Pdf.value.generatePdf();
};
</script>

<style lang="scss">
#templateCard {
  border: 2px solid white;
  padding: 10px;
  border-radius: 10px;
  width: 100%;
  height: 100%;
}
</style>
