<template>
  <section>
    <TheHero />
    <section class="section-form">
      <div class="container">
        <TheForm @user-data="checkData" />
        <TheCan @user-info="check" />
        <TheCant @user-info="check" />
      </div>
    </section>
    <TheTable :sendingData="sendingData" />
  </section>
</template>

<script>
import TheHero from "./components/TheHero.vue";
import TheForm from "./components/TheForm.vue";
import TheCan from "./components/TheCan.vue";
import TheCant from "./components/TheCant.vue";
import TheTable from "./components/TheTable.vue";

export default {
  name: "App",
  components: {
    TheHero,
    TheForm,
    TheCan,
    TheCant,
    TheTable,
  },

  data() {
    return {
      userInfo: {},
      userData: {},
      sendingData: {},
    };
  },

  methods: {
    check(userInfo) {
      this.userInfo = {
        usedLangs: userInfo.usedLangs,
        favoriteLang: userInfo.favoriteLang,
        whyLearn: userInfo.whyLearn,
        whyNot: userInfo.whyNot,
        learnFirst: userInfo.learnFirst,
        learnToday: userInfo.learnToday,
      };
      this.checkAll();
    },

    checkData(userData) {
      this.userData = {
        firstName: userData.firstName,
        lastName: userData.lastName,
        email: userData.email,
        job: userData.job,
        code: userData.code,
        nameIsValid: userData.nameIsValid,
        lastIsValid: userData.lastIsValid,
        emailIsValid: userData.emailIsValid,
      };
    },

    checkAll() {
      let regex = /^[A-Za-z]+$/;
      let regexEmail =
        /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;

      if (
        !this.userData.firstName.match(regex) &&
        !document
          .querySelectorAll(".invalid-info")[0]
          .classList.contains("invalid")
      ) {
        document.querySelectorAll(".invalid-info")[0].classList.add("invalid");
      }

      if (this.userData.firstName.match(regex)) {
        document
          .querySelectorAll(".invalid-info")[0]
          .classList.remove("invalid");
        this.userData.nameIsValid = true;
      }

      if (
        !this.userData.lastName.match(regex) &&
        !document
          .querySelectorAll(".invalid-info")[1]
          .classList.contains("invalid")
      ) {
        document.querySelectorAll(".invalid-info")[1].classList.add("invalid");
      }

      if (this.userData.lastName.match(regex)) {
        document
          .querySelectorAll(".invalid-info")[1]
          .classList.remove("invalid");
        this.userData.lastIsValid = true;
      }

      if (
        !this.userData.email.match(regexEmail) &&
        !document
          .querySelectorAll(".invalid-info")[2]
          .classList.contains("invalid")
      ) {
        document.querySelectorAll(".invalid-info")[2].classList.add("invalid");
      }

      if (this.userData.lastName.match(regexEmail)) {
        document
          .querySelectorAll(".invalid-info")[2]
          .classList.remove("invalid");
        this.userData.emailIsValid = true;
      }

      if (
        this.userData.emailIsValid &&
        this.userData.firstName &&
        this.userData.lastName
      ) {
        this.showTable();
      }
    },
    showTable() {
      document.querySelector(".section-hero").classList.add("hidden");
      document.querySelector(".section-form").classList.add("hidden");
      document.querySelector(".section-table").classList.remove("hidden");
      console.log(this.userData);
      console.log(this.userInfo);
      if (this.userData.code === true) this.userData.code = "Yes";
      if (this.userData.code === false) this.userData.code = "No";
      if (this.userInfo.learnToday === true) this.userInfo.learnToday = "Yes";
      if (this.userInfo.learnToday === false) this.userInfo.learnToday = "No";
      this.sendingData = {
        ...this.userData,
        ...this.userInfo,
      };
    },
  },
};
</script>

<style>
@import "../public/styles/css/general.css";
@import "../public/styles/css/style.css";
</style>
