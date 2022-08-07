<template>
  <div id="templateCard" :style="bgColor">
    <div class="actions">
      <div class="title"><h4>Customization</h4></div>
      <div class="operations">
        <div class="bgColor">
          <input id="bgcolor" type="color" :value="bgColor['--bg-color']" @change="changebgColor" />
          <label for="bgcolor">Theme Color</label>
        </div>

        <div class="textColor">
          <input
            id="textcolor"
            type="color"
            :value="bgColor['--font-color']"
            @change="changefontColor"
          />
          <label for="textcolor">Text Color</label>
        </div>
      </div>
      <BaseBtnVue class="generateBtn" type="success" @click="generateReport">Generate</BaseBtnVue>
    </div>

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
  </div>
</template>

<script setup lang="ts">
import Vue3Html2pdf from "vue3-html2pdf";
import BaseBtnVue from "./BaseBtn.vue";
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

<style lang="scss" scoped>
#templateCard {
  border: 2px solid white;
  padding: 10px;
  border-radius: 10px;
  width: 100%;
  height: 100%;
}

.actions {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  background-color: white;
  margin-bottom: 10px;
  border-radius: 10px 10px 0 0;
  box-shadow: $shadow;

  .operations {
    display: inline-flex;
    width: 100%;
    justify-content: space-around;
    align-items: baseline;
    margin-bottom: 20px;

    label {
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;
      font-size: 12px;
      font-weight: bold;
      margin-right: 5px;
    }

    input[type="color"]::-webkit-color-swatch {
      border: none;
    }

    input {
      cursor: pointer;
      border-radius: 50%;
      width: 40px;
      height: 40px;
      padding: 5px;
      margin-bottom: 10px;
    }

    .bgColor input {
      background-color: var(--bg-color);
    }

    .textColor input {
      background-color: var(--font-color);
    }
  }
  .generateBtn {
    width: 100%;
  }
}
</style>
