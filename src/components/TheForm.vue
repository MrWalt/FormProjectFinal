<template>
  <div class="form-container hidden inactive" id="section-form">
    <div class="form-img-box" @click="sendInfo"></div>
    <form class="form" autocomplete="off" @click="sendInfo">
      <div class="form-box">
        <label class="important-info" for="first-name">First Name</label>
        <input
          type="text"
          id="first-name"
          v-model="firstName"
          placeholder="John"
        />
        <p class="invalid-info">Invalid info</p>
      </div>
      <div class="form-box">
        <label class="important-info" for="last-name">Last Name</label>
        <input
          type="text"
          id="last-name"
          v-model="lastName"
          placeholder="Smith"
        />
        <p class="invalid-info">Invalid info</p>
      </div>
      <div class="form-box">
        <label class="important-info" for="email">Email Address</label>
        <input
          type="text"
          id="email"
          v-model="email"
          placeholder="johnsmith@example.com"
        />
        <p class="invalid-info">Invalid info</p>
      </div>
      <div class="form-box">
        <label for="job">Current Job</label>
        <input type="text" id="job" v-model="job" placeholder="Developer" />
      </div>
      <div class="form-box-checkbox">
        <p>Can you code?</p>
        <div class="form-checkbox">
          <div class="form-option">
            <div class="form-btn" @click="canCode"></div>
            <label>Yes</label>
          </div>
          <div class="form-option">
            <div class="form-btn" @click="cantCode"></div>
            <label>No</label>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "TheForm",
  data() {
    return {
      firstName: "",
      lastName: "",
      email: "",
      job: "",
      code: "",
      isValid: "",
    };
  },

  methods: {
    sendInfo() {
      if (this.firstName) this._checkFirst();
      if (this.lastName) this._checkLast();
      if (this.email) this._checkEmail();
      let finalCheck = [...document.querySelectorAll(".invalid-info")];
      if (finalCheck.some((el) => el.classList.contains("invalid"))) {
        return;
      }

      const userInfo = {
        firstName: this.firstName,
        lastName: this.lastName,
        email: this.email,
        job: this.job,
        code: this.code,
        nameIsValid: this.nameIsValid,
        lastIsValid: this.lastIsValid,
        emailIsValid: this.emailIsValid,
      };

      this.$emit("user-data", userInfo);
    },

    observer() {
      let options = {
        root: null,
        rootMargin: "0px",
        threshold: 0.9,
      };
      const observer = new IntersectionObserver(this.sendInfo, options);
      observer.observe(document.querySelector("#can-code"));
      observer.observe(document.querySelector("#cant-code"));
    },

    _checkFirst() {
      let regex = /^[A-Za-z]+$/;

      if (
        !this.firstName.match(regex) &&
        !document
          .querySelectorAll(".invalid-info")[0]
          .classList.contains("invalid")
      ) {
        document.querySelectorAll(".invalid-info")[0].classList.add("invalid");
        this.nameIsValid = false;
        return;
      }

      if (this.firstName.match(regex)) {
        document
          .querySelectorAll(".invalid-info")[0]
          .classList.remove("invalid");
        this.nameIsValid = true;
        return true;
      }
    },

    _checkLast() {
      let regex = /^[A-Za-z]+$/;

      if (
        !this.lastName.match(regex) &&
        !document
          .querySelectorAll(".invalid-info")[1]
          .classList.contains("invalid")
      ) {
        document.querySelectorAll(".invalid-info")[1].classList.add("invalid");
        this.lastIsValid = false;
        return;
      }

      if (this.lastName.match(regex)) {
        document
          .querySelectorAll(".invalid-info")[1]
          .classList.remove("invalid");
        this.lastIsValid = true;
        return true;
      }
    },

    _checkEmail() {
      let regex =
        /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;

      if (
        !this.email.match(regex) &&
        !document
          .querySelectorAll(".invalid-info")[2]
          .classList.contains("invalid")
      ) {
        document.querySelectorAll(".invalid-info")[2].classList.add("invalid");
        this.emailIsValid = false;
        return;
      }

      if (this.email.match(regex)) {
        document
          .querySelectorAll(".invalid-info")[2]
          .classList.remove("invalid");
        this.emailIsValid = true;
        return true;
      }
    },
    canCode() {
      if (
        !document
          .querySelectorAll(".form-btn")[1]
          .classList.contains("check-active")
      ) {
        document.querySelectorAll(".form-btn")[0].classList.add("check-active");
        document
          .querySelector(".form-dropdown-can-code")
          .classList.remove("hidden");
        setTimeout(function () {
          document
            .querySelector(".form-dropdown-can-code")
            .classList.add("active-form");
        }, 100);
        setTimeout(function () {
          document
            .querySelector(".form-dropdown-can-code")
            .classList.remove("index");
        }, 400);
        this._scrollView(document.querySelector("#can-code"));

        this.code = true;
        this.observer();
        return;
      }
      document
        .querySelectorAll(".form-btn")[1]
        .classList.remove("check-active");
      document
        .querySelector(".form-dropdown-cant-code")
        .classList.add("hidden");
      document.querySelector(".form-dropdown-cant-code").classList.add("index");
      document
        .querySelector(".form-dropdown-cant-code")
        .classList.remove("active-form");
      document.querySelectorAll(".form-btn")[0].classList.add("check-active");
      document
        .querySelector(".form-dropdown-can-code")
        .classList.remove("hidden");
      setTimeout(function () {
        document
          .querySelector(".form-dropdown-can-code")
          .classList.add("active-form");
      }, 100);
      setTimeout(function () {
        document
          .querySelector(".form-dropdown-can-code")
          .classList.remove("index");
      }, 400);
      this._scrollView(document.querySelector("#can-code"));
      this.observer();
      this.code = true;
    },
    cantCode() {
      if (
        !document
          .querySelectorAll(".form-btn")[0]
          .classList.contains("check-active")
      ) {
        document.querySelectorAll(".form-btn")[1].classList.add("check-active");
        document
          .querySelector(".form-dropdown-cant-code")
          .classList.remove("hidden");
        setTimeout(function () {
          document
            .querySelector(".form-dropdown-cant-code")
            .classList.add("active-form");
        }, 100);
        setTimeout(function () {
          document
            .querySelector(".form-dropdown-cant-code")
            .classList.remove("index");
        }, 400);
        this._scrollView(document.querySelector("#cant-code"));
        this.code = false;
        this.observer();
        return;
      }
      document
        .querySelectorAll(".form-btn")[0]
        .classList.remove("check-active");
      document.querySelector(".form-dropdown-can-code").classList.add("hidden");
      document.querySelector(".form-dropdown-can-code").classList.add("index");
      document
        .querySelector(".form-dropdown-can-code")
        .classList.remove("active-form");
      document.querySelectorAll(".form-btn")[1].classList.add("check-active");
      document
        .querySelector(".form-dropdown-cant-code")
        .classList.remove("hidden");
      setTimeout(function () {
        document
          .querySelector(".form-dropdown-cant-code")
          .classList.add("active-form");
      }, 100);
      setTimeout(function () {
        document
          .querySelector(".form-dropdown-cant-code")
          .classList.remove("index");
      }, 400);
      this._scrollView(document.querySelector("#cant-code"));
      this.observer();
      this.code = false;
    },
    _scrollView(element) {
      setTimeout(function () {
        element.scrollIntoView({ behavior: "smooth" });
      }, 300);
    },
  },
};
</script>
