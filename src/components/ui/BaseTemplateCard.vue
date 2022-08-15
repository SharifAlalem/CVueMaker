<template>
  <div id="templateCard" :style="bgColor">
    <PdfCustomizationVue />
    <Vue3Html2pdf
      :show-layout="pdfOptions.showLayout"
      :float-layout="pdfOptions.floatLayout"
      :enable-download="pdfOptions.enableDownload"
      :preview-modal="pdfOptions.previewModal"
      :filename="pdfOptions.filename"
      :paginate-elements-by-height="pdfOptions.paginateElementsByHeight"
      :pdf-quality="pdfOptions.pdfQuality"
      :pdf-format="pdfOptions.pdfFormat"
      :pdf-orientation="pdfOptions.pdfOrientation"
      :pdf-content-width="pdfOptions.pdfContentWidth"
      :manual-pagination="pdfOptions.manualPagination"
      @progress="onProgress($event)"
      @startPagination="startPagination()"
      @hasPaginated="hasPaginated()"
      ref="html2Pdf"
    >
      <template #pdf-content :style="`width: ${pdfOptions.pdfContentWidth};`">
        <slot></slot>
      </template>
    </Vue3Html2pdf>
  </div>
</template>

<script setup lang="ts">
import Vue3Html2pdf from "vue3-html2pdf";
import PdfCustomizationVue from "./PdfCustomization.vue";
import { ref, reactive, provide, inject } from "vue";

const personalInfoData: any = inject("personalInfoData");
//theme dynamic change color
let bgColor: any = reactive({ "--bg-color": "#0930A5", "--font-color": "#ffffff" });

const changebgColor = ($event: any) => {
  bgColor["--bg-color"] = $event.target.value;
};
const changefontColor = ($event: any) => {
  bgColor["--font-color"] = $event.target.value;
};

provide("bgColor", bgColor);
provide("changebgColor", changebgColor);
provide("changefontColor", changefontColor);
//===========================

//html2pdf
let pdfOptions: any = reactive({
  showLayout: false,
  floatLayout: false,
  enableDownload: true,
  previewModal: false,
  paginateElementsByHeight: 2500,
  manualPagination: true,
  filename: personalInfoData.find((input: any) => input.inputName === "fname")["fname"],
  pdfQuality: 2,
  pdfFormat: "a4",
  pdfOrientation: "portrait",
  pdfContentWidth: "100%",
});

const updateField = (key: any, newValue: any) => {
  pdfOptions[key] = newValue;
};
provide("updateField", updateField);
provide("manualPagination", pdfOptions);

let html2Pdf: any = ref(null);
let pdfContent: any = ref(null);
const updatepdfContent = (newValue: any) => {
  pdfContent.value = newValue;
};
provide("updatepdfContent", updatepdfContent);
const progress = ref(0);
const hasAlreadyParsed = ref(false);
const generatePdf = () => {
  startPagination();
  progress.value = 0;
  paginationOfElements();
};
const downloadPdf = async () => {
  html2Pdf.value.generatePdf();
};
const onProgress: any = (thisprogress: any) => {
  progress.value = thisprogress;
  console.log(`PDF generation progress: ${progress.value}%`);
};
const startPagination = () => {
  console.log(`PDF has started pagination`);
};

const hasPaginated = () => {
  console.log(`PDF has been paginated`);
};
const paginationOfElements = () => {
  progress.value = 25;

  /*
				When this props is true,
				the props paginate-elements-by-height will not be used.
				Instead the pagination process will rely on the elements with a class "html2pdf__page-break"
				to know where to page break, which is automatically done by html2pdf.js
			*/
  if (pdfOptions.manualPagination) {
    progress.value = 70;
    downloadPdf();
    return;
  }

  if (!hasAlreadyParsed.value) {
    const parentElement = pdfContent.value.firstChild;
    const ArrOfContentChildren = Array.from(parentElement.children);
    let childrenHeight = 0;

    /*
					Loop through Elements and add there height with childrenHeight variable.
					Once the childrenHeight is >= this.paginateElementsByHeight, create a div with
					a class named 'html2pdf__page-break' and insert the element before the element
					that will be in the next page
				*/
    for (const childElement of ArrOfContentChildren) {
      // Get The First Class of the element
      const elementFirstClass = childElement.classList[0];
      const isPageBreakClass = elementFirstClass === "html2pdf__page-break";
      if (isPageBreakClass) {
        childrenHeight = 0;
      } else {
        // Get Element Height
        const elementHeight = childElement.clientHeight;

        // Get Computed Margin Top and Bottom
        const elementComputedStyle =
          childElement.currentStyle || window.getComputedStyle(childElement);
        const elementMarginTopBottom = 1100;
        parseInt(elementComputedStyle.marginTop) + parseInt(elementComputedStyle.marginBottom);

        // Add Both Element Height with the Elements Margin Top and Bottom
        const elementHeightWithMargin = elementHeight + elementMarginTopBottom;

        if (childrenHeight + elementHeight < pdfOptions.paginateElementsByHeight) {
          childrenHeight += elementHeightWithMargin;
        } else {
          const section = document.createElement("div");
          section.classList.add("html2pdf__page-break");
          parentElement.insertBefore(section, childElement);

          // Reset Variables made the upper condition false
          childrenHeight = elementHeightWithMargin;
        }
      }
    }

    progress.value = 70;

    /*
					Set to true so that if would generate again we wouldn't need
					to parse the HTML to paginate the elements
				*/
    hasAlreadyParsed.value = true;
  } else {
    progress.value = 70;
  }

  hasPaginated();
  downloadPdf();
};
provide("progress", progress);
provide("generateReport", generatePdf);
//===========================
</script>

<style lang="scss">
@import "../../assets/styles/mixins";

#templateCard {
  border: 2px solid white;
  border-radius: 10px;
  width: 100%;
  height: 100%;
  background-color: white;
  z-index: 999;

  @media (max-width: $breakpoint-mobile) {
    width: 98%;
  }
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
  font-size: 12px;

  .operations {
    display: inline-flex;
    width: 100%;
    justify-content: center;
    align-items: center;
    flex-wrap: wrap;
    gap: 10px;
    margin-bottom: 20px;

    .control-item {
      width: 15%;
      @media (max-width: $breakpoint-tablet) {
        width: 40%;
      }
      @media (max-width: $breakpoint-mobile) {
        width: 100%;
      }
    }
    label {
      display: flex;
      flex-direction: row;
      justify-content: center;
      align-items: center;

      font-weight: bold;
      margin-right: 5px;
    }

    input,
    select {
      padding: 5px;
      margin-bottom: 10px;
      width: 90%;
      border: 2px solid lightgrey;
      color: #333;
      background-color: #fff;
      border-radius: 4px;
      font-size: 14px;

      &:focus {
        border: 2px solid $blue;
        outline: none;
        @include shadow_color(rgb(80, 191, 255, 0.2));
      }
    }
    input[type="color"]::-webkit-color-swatch {
      border: none;
    }

    input[type="color"],
    input[type="checkbox"] {
      cursor: pointer;
      width: 25px;
      height: 25px;
    }

    .bgColor input {
      background-color: var(--bg-color);
    }

    .textColor input {
      background-color: var(--font-color);
    }
  }

  .generateBtn {
    width: 250px;

    .icon {
      margin-right: 15px;
    }
  }
}
</style>
