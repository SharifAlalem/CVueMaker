<template>
  <template class="container" :style="bgColor">
    <aside>
      <div class="image">
        <img :src="personalData.avatarImg" alt="avatar" width="100" />
      </div>
      <div class="contact">
        <h1>Contact Me</h1>
        <ul>
          <li>
            <span class="icon"> <i class="fa-location-pin fa-solid"></i> </span
            ><span class="text"
              >{{ personalData.streetAndNum }} , {{ personalData.city }},{{ personalData.country }}
            </span>
          </li>
          <li>
            <span class="icon"> <i class="fa-phone fa-solid"></i> </span
            ><span class="text">{{ personalData.phone }} </span>
          </li>
          <li>
            <span class="icon"> <i class="fa-at fa-solid"></i> </span
            ><span class="text">{{ personalData.email }} </span>
          </li>
        </ul>
      </div>
      <div class="social">
        <h1>Social Links</h1>
        <ul>
          <li>
            <span class="icon"> <i class="fa-circle fa-solid"></i> </span
            ><span class="text">text text text</span>
          </li>
          <li>
            <span class="icon"> <i class="fa-circle fa-solid"></i> </span
            ><span class="text">text text text</span>
          </li>
          <li>
            <span class="icon"> <i class="fa-circle fa-solid"></i> </span
            ><span class="text">text text text</span>
          </li>
        </ul>
      </div>
      <div class="other">
        <h1>Other Info</h1>
        <div class="skills">
          <h2>skills</h2>
        </div>
        <div class="awards">
          <h2>awards</h2>
        </div>
        <div class="languages">
          <h2>languages</h2>
        </div>
        <div class="interests">
          <h2>interests</h2>
        </div>
      </div>
    </aside>
    <main>
      <div class="personal">
        <h1>{{ personalData.fname }} {{ personalData.lname }}</h1>
        <h3>{{ personalData.profession }}</h3>
      </div>
      <div class="about">
        <h1>about me</h1>
        <p>{{ personalData.summary }}</p>
      </div>
      <div class="work">
        <h1>Experience</h1>
        <ul>
          <li>
            <span class="date">2018-2019 </span><span class="companyName">text text </span>
            <span class="jobTitle">| text text </span>
            <div class="responseabilties">
              <ul>
                <li>text</li>
                <li>text</li>
                <li>text</li>
                <li>text</li>
              </ul>
            </div>
          </li>
          <li>
            <span class="date">2018-2019 </span><span class="companyName">text text </span>
            <span class="jobTitle">| text text </span>
            <div class="responseabilties">
              <ul>
                <li>text</li>
                <li>text</li>
                <li>text</li>
                <li>text</li>
              </ul>
            </div>
          </li>
          <li>
            <span class="date">2018-2019 </span><span class="companyName">text text </span>
            <span class="jobTitle">| text text </span>
            <div class="responseabilties">
              <ul>
                <li>text</li>
                <li>text</li>
                <li>text</li>
                <li>text</li>
              </ul>
            </div>
          </li>
        </ul>
      </div>
      <div class="education">
        <h1>Eduction</h1>
        <ul>
          <li>
            <span class="date">2018-2019 </span>
            <span class="degreeTitle"> text text </span>
            <span class="educationName">| text text </span>
          </li>
          <li>
            <span class="date">2018-2019 </span>
            <span class="degreeTitle"> text text </span>
            <span class="educationName">| text text </span>
          </li>
          <li>
            <span class="date">2018-2019 </span>
            <span class="degreeTitle"> text text </span>
            <span class="educationName">| text text </span>
          </li>
        </ul>
      </div>
      <div class="projects">
        <h1>Projects</h1>
        <ul>
          <li>
            <span class="date">2018-2019 </span><span class="companyName">text text </span>
            <span class="jobTitle">| text text </span>
            <div class="responseabilties">
              <ul>
                <li>text</li>
                <li>text</li>
                <li>text</li>
                <li>text</li>
              </ul>
            </div>
          </li>
          <li>
            <span class="date">2018-2019 </span><span class="projectName">text text </span>
            <div class="features">
              <ul>
                <li>text</li>
                <li>text</li>
                <li>text</li>
                <li>text</li>
              </ul>
            </div>
          </li>
        </ul>
      </div>
    </main>
    <footer>developed by sharif Alalem</footer>
  </template>
</template>
<script setup lang="ts">
import { inject } from "vue";
let bgColor: any = inject("bgColor");
const personalInfoData: any = inject("personalInfoData");

let personalData = {
  avatarImg: personalInfoData.find((input: any) => input.inputName === "avatarImg").avatarImg,
  fname: personalInfoData.find((input: any) => input.inputName === "fname").fname,
  lname: personalInfoData.find((input: any) => input.inputName === "lname").lname,
  phone: personalInfoData.find((input: any) => input.inputName === "phone").phone,
  email: personalInfoData.find((input: any) => input.inputName === "email").email,
  streetAndNum: personalInfoData.find((input: any) => input.inputName === "streetAndNum")
    .streetAndNum,
  city: personalInfoData.find((input: any) => input.inputName === "city").city,
  country: personalInfoData.find((input: any) => input.inputName === "country").country,
  dateOfBirth: personalInfoData.find((input: any) => input.inputName === "dateOfBirth").dateOfBirth,
  profession: personalInfoData.find((input: any) => input.inputName === "profession").profession,
  summary: personalInfoData.find((input: any) => input.inputName === "summary").summary,
};
</script>

<style lang="scss" scoped>
@import "../../assets/styles/mixins";

.actions {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin: 50px 0;
}
button {
  z-index: 999999999999;
  cursor: pointer;
}

.container {
  width: 100%;
  display: grid;
  grid-template-columns: 0.3fr 1fr;
  grid-template-rows: 10fr 0.1fr;
  grid-template-areas:
    "aside main"
    "footer footer";
}

main {
  @include color_scheme(white, black);
  grid-area: main;
  padding: 10%;
  display: flex;
  text-align: left;
  justify-content: center;
  flex-direction: column;
  align-items: start;

  div {
    margin-bottom: 30px;
  }

  .personal {
    h1 {
      font-size: 40px;
      text-decoration: none;
    }

    h3 {
      font-size: 20px;
    }
  }

  h1 {
    color: var(--bg-color);
    text-transform: uppercase;
    font-size: 16px;
    margin: 0;
    text-decoration: underline;
  }
}
aside {
  @include color_scheme(var(--bg-color), var(--font-color));
  grid-area: aside;
  text-align: left;
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;

  div {
    margin-bottom: 30px;
  }

  .image {
    text-align: center;
  }

  h1 {
    text-transform: uppercase;
    text-decoration: underline;
    font-size: 16px;
    margin: 0;
  }

  h2 {
    text-transform: uppercase;
    font-size: 13px;
    margin: 5xp 0;
  }
  ul {
    list-style: none;
    padding: 0 5px;
    margin: 0;

    li {
      margin: 10px 0;
    }
    .icon {
      font-size: 12px;
      margin-right: 5px;
    }
    .text {
      font-size: 12px;
    }
  }
}
footer {
  @include color_scheme(black, white);
  grid-area: footer;
  padding: 5px 0;
  font-size: 10px;
  font-family: "Arial Narrow", Arial, sans-serif;
}
</style>
