<template>
  <div>
    <div class="actions">
      <div class="title"><h4>Customization</h4></div>
      <div class="operations">
        <div class="control-item" v-for="(control, key) in controls" :key="key">
          <div class="control">
            <select
              v-if="control.vModel === 'pdfOrientation' || control.vModel === 'pdfFormat'"
              :value="control.options[0]"
              @change="setInput($event, control.vModel, control.inputType)"
            >
              <option v-for="opt in control.options" :value="opt" :key="opt">{{ opt }}</option>
            </select>

            <input
              v-else
              :class="control.inputType === 'checkbox' ? 'input-checkbox' : 'input-box'"
              :type="control.inputType"
              :value="control.value"
              :checked="control.value"
              @input="setInput($event, control.vModel, control.inputType)"
              @change="setInput($event, control.vModel, control.inputType)"
            />
            <label>
              {{ control.label }}
            </label>
          </div>
        </div>

        <div class="bgColor control-item">
          <input id="bgcolor" type="color" :value="bgColor['--bg-color']" @change="changebgColor" />
          <label for="bgcolor">Theme Color</label>
        </div>
        <div class="textColor control-item">
          <input
            id="textcolor"
            type="color"
            :value="bgColor['--font-color']"
            @change="changefontColor"
          />
          <label for="textcolor">Text Color</label>
        </div>
      </div>

      <BaseBtnVue :disabled="false" class="generateBtn" type="download" @click="generateReport">
        <i class="fa-solid fa-file-arrow-down icon"></i>Generate PDF
      </BaseBtnVue>

      <div class="progress-container">
        <div class="generating-label" v-if="progress !== 0">
          <span class="label-title">
            {{ progress === 100 ? "PDF Generated" : "Generating PDF" }}
          </span>

          <span class="label-progress">
            {{ `${progress} %` }}
          </span>
        </div>
        <div class="progress-bar">
          <div class="progress" :style="`width: ${progress}%;`" />
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, inject } from "vue";
import BaseBtnVue from "./BaseBtn.vue";

const changefontColor: any = inject("changefontColor");
const changebgColor: any = inject("changebgColor");
const updateField: any = inject("updateField");
const bgColor: any = inject("bgColor");
const progress: any = inject("progress");
const generateReport: any = inject("generateReport");
const state: any = inject("manualPagination");

let controls = reactive([
  {
    label: "paginate-elements-by-height",
    type: "Number",
    options: "Any Number",
    inputType: "number",
    vModel: "paginateElementsByHeight",
    value: state.paginateElementsByHeight,
  },

  //   {
  //     label: "filename",
  //     type: "String",
  //     options: "Any String",
  //     inputType: "text",
  //     vModel: "filename",
  //   },

  //   {
  //     label: "pdf-quality",
  //     type: "Number",
  //     options: "0 - 2 (Can Have Decimal)",
  //     inputType: "number",
  //     vModel: "pdfQuality",
  //   },

  {
    label: "pdf-format",
    type: "String",
    options: ["a4", "a0", "a1", "a2", "a3", "letter", "legal", "a5", "a6", "a7", "a8", "a9", "a10"],
    inputType: "text",
    vModel: "pdfFormat",
    value: "a4",
  },

  {
    label: "pdf-orientation",
    type: "String",
    options: ["portrait", "landscape"],
    inputType: "text",
    vModel: "pdfOrientation",
    value: "portrait",
  },

  //   {
  //     label: "pdf-content-width",
  //     type: "String",
  //     options: 'Any css sizes (e.g. "800px", "65vw", "70%")',
  //     inputType: "text",
  //     vModel: "pdfContentWidth",
  //   },
  //   {
  //     label: "show-layout",
  //     type: "",
  //     options: "",
  //     inputType: "checkbox",
  //     vModel: "showLayout",
  //   },

  //   {
  //     label: "float-layout",
  //     type: "",
  //     options: "true, false",
  //     inputType: "checkbox",
  //     vModel: "floatLayout",
  //   },

  //   {
  //     label: "enable-download",
  //     type: "",
  //     options: "true, false",
  //     inputType: "checkbox",
  //     vModel: "enableDownload",
  //   },

  //   {
  //     label: "preview-modal",
  //     type: "",
  //     options: "true, false",
  //     inputType: "checkbox",
  //     vModel: "previewModal",
  //   },

  {
    label: "manual-pagination",
    type: "",
    options: "true, false",
    inputType: "checkbox",
    vModel: "manualPagination",
    value: true,
  },
]);

const isGenerating = () => {
  return progress !== 0 || progress !== 100;
};

const setInput = (e: any, key: any, inputType: any) => {
  let value = e.target.value;

  if (inputType === "checkbox") {
    value = e.target.checked;
  }

  if (inputType === "number") {
    value = e.target.value ? parseFloat(e.target.value) : 0;
  }

  updateField(key, value);
};
</script>

<style lang="scss" scoped>
.progress-container {
  width: 100%;
  margin-top: 10px;
  text-align: center;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  border-radius: 20px;

  .progress-bar {
    width: 100%;
    height: 10px;
    border-radius: 10px 10px 0 0;
    border: 2px solid $light-gray;

    .progress {
      width: 0%;
      height: 100%;
      transition: 0.3s;
      border-radius: 10px 10px 0 0;
      background: $dark-blue;
    }
  }
}
</style>
