<template>
  <TheHeader :logo="require('@/assets/images/logo.png')" :type="'transparent'" :links="links" />
  <router-view />
  <TheFooter :type="'solid'" :social="social" />
</template>

<script setup lang="ts">
import TheHeader from "@/components/layouts/TheHeader.vue";
import TheFooter from "@/components/layouts/TheFooter.vue";
import { reactive, provide, ref } from "vue";

let links: { url: string; name: string }[] = [
  { url: "/", name: "Home" },
  { url: "/about", name: "About" },
];

let social: { icon: string; link: string }[] = [
  { icon: "test", link: "Home" },
  { icon: "test", link: "About" },
];

//DATA

let personalImage = ref("");
const changeImage = (newImage: any) => {
  console.log("newImage", newImage.value);
  personalImage.value = newImage.value;
};
provide("changeImage", changeImage);

let personalInfoData = reactive([
  {
    inputName: "fname",
    fname: "",
    type: "string",
    placeholder: " first name ",
    width: "medium",
  },
  {
    inputName: "lname",
    lname: "",
    type: "string",
    placeholder: " last name ",
    width: "medium",
  },
  {
    inputName: "phone",
    phone: "",
    type: "string",
    placeholder: " phone number ",
    width: "full",
  },
  {
    inputName: "email",
    email: "",
    type: "email",
    placeholder: " email address ",
    width: "full",
  },
  {
    inputName: "streetAndNum",
    streetAndNum: "",
    type: "string",
    placeholder: " street name and number ",
    width: "full",
  },
  {
    inputName: "city",
    city: "",
    type: "string",
    placeholder: " city ",
    width: "medium",
  },
  {
    inputName: "country",
    country: "",
    type: "string",
    placeholder: " country ",
    width: "medium",
  },
  {
    inputName: "dateOfBirth",
    dateOfBirth: "",
    type: "date",
    placeholder: "",
    width: "full",
  },
  {
    inputName: "profession",
    profession: "",
    type: "string",
    placeholder: " profession ",
    width: "full",
  },
  {
    inputName: "summary",
    summary: "",
    type: "textarea",
    placeholder: "summary",
    width: "full",
  },
]);

let educationInfoData = reactive({
  forms: [
    {
      id: 1,
      data: [
        {
          inputName: "degreeTitle",
          degreeTitle: "",
          type: "string",
          placeholder: " Degree Title",
          width: "full",
        },
        {
          inputName: "college",
          college: "",
          type: "string",
          placeholder: " College / University",
          width: "full",
        },
        {
          inputName: "startDate",
          startDate: "",
          type: "date",
          placeholder: " ",
          width: "medium",
        },
        {
          inputName: "endDate",
          endDate: "",
          type: "date",
          placeholder: "",
          width: "medium",
        },
      ],
    },
  ],
});

let workInfoData = reactive({
  forms: [
    {
      id: 1,
      data: [
        {
          inputName: "jobTitle",
          jobTitle: "",
          type: "string",
          placeholder: " job Title",
          width: "full",
        },
        {
          inputName: "companyName",
          companyName: "",
          type: "string",
          placeholder: " Company Name",
          width: "full",
        },
        {
          inputName: "startDate",
          startDate: "",
          type: "date",
          placeholder: " ",
          width: "medium",
        },
        {
          inputName: "endDate",
          endDate: "",
          type: "date",
          placeholder: "",
          width: "medium",
        },
        {
          inputName: "summary",
          summary: "",
          type: "textarea",
          placeholder: " Summary",
          width: "full",
        },
      ],
    },
  ],
});

let projectInfoData = reactive({
  forms: [
    {
      id: 1,
      data: [
        {
          inputName: "projectTitle",
          projectTitle: "",
          type: "string",
          placeholder: " Project Title",
          width: "full",
        },
        {
          inputName: "companyName",
          companyName: "",
          type: "string",
          placeholder: " Company Name",
          width: "full",
        },
        {
          inputName: "startDate",
          startDate: "",
          type: "date",
          placeholder: " ",
          width: "medium",
        },
        {
          inputName: "endDate",
          endDate: "",
          type: "date",
          placeholder: "",
          width: "medium",
        },
        {
          inputName: "description",
          description: "",
          type: "textarea",
          placeholder: " Description",
          width: "full",
        },
      ],
    },
  ],
});

let skillInfoData = reactive({
  forms: [
    {
      id: 1,
      data: [
        {
          inputName: "skillTitle",
          skillTitle: "",
          type: "string",
          placeholder: " Skill Title",
          width: "full",
        },
        {
          inputName: "rating",
          rating: 1,
          type: "rating",
          placeholder: "",
          width: "full",
        },
      ],
    },
  ],
});

let templatesInfoData = reactive([
  {
    templateId: 1,
    imageUrl: "skillTitle",
    selected: false,
  },
  {
    templateId: 1,
    imageUrl: "skillTitle",
    selected: false,
  },
]);

const changeRating = (index: number, formId: number) => {
  skillInfoData.forms[formId - 1].data.forEach((input) => {
    if (input.rating !== undefined) input.rating = index + 1;
  });
};

const chooseTemplate = (templateId: number) => {
  templatesInfoData.forEach((template) => {
    if (template.templateId === templateId) template.selected = true;
  });
};

const updateFormsData = (newForm: any, formType: string) => {
  if (formType === "education") educationInfoData.forms.push(newForm);
  else if (formType === "work") workInfoData.forms.push(newForm);
  else if (formType === "project") projectInfoData.forms.push(newForm);
  else if (formType === "skill") skillInfoData.forms.push(newForm);
};

const removeFormsData = (id: any, formType: string) => {
  if (formType === "education")
    educationInfoData.forms = educationInfoData.forms.filter((educationBlock) => {
      return educationBlock.id !== id;
    });
  else if (formType === "work")
    workInfoData.forms = workInfoData.forms.filter((workBlock) => {
      return workBlock.id !== id;
    });
  else if (formType === "project")
    projectInfoData.forms = projectInfoData.forms.filter((projectBlock) => {
      return projectBlock.id !== id;
    });
  else if (formType === "skill")
    skillInfoData.forms = skillInfoData.forms.filter((skillBlock) => {
      return skillBlock.id !== id;
    });
};

//providing Data
provide("personalImage", personalImage);
provide("personalInfoData", personalInfoData);
provide("educationInfoData", educationInfoData);
provide("workInfoData", workInfoData);
provide("projectInfoData", projectInfoData);
provide("skillInfoData", skillInfoData);
provide("templatesInfoData", templatesInfoData);
//providing Functions
provide("changeRating", changeRating);
provide("chooseTemplate", chooseTemplate);
provide("updateFormsData", updateFormsData);
provide("removeFormsData", removeFormsData);
</script>

<style lang="scss">
html,
body {
  margin: 0;
}

#app {
  font-family: "Open Sans", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: linear-gradient(90deg, #1cb5e0 0%, #000851 100%);
}

.title {
  font-size: $title-font;
  text-transform: uppercase;
}
</style>
