<template>
  <div
    class="form-dropdown-cant-code form-dropdown index hidden"
    id="cant-code"
  >
    <div class="dropdown-heading">
      <h2 class="heading-secondary">Tell us more</h2>
      <p class="subheading">Its gonna be quick</p>
    </div>
    <form autocomplete="off" class="dropdown-container">
      <div class="form-box">
        <label for="ask-why">Why not?</label>
        <input
          type="text"
          v-model="whyNot"
          id="ask-why"
          placeholder="No free time"
        />
      </div>
      <div class="form-box">
        <label for="learn-first">What language would you learn first?</label>
        <input
          type="text"
          v-model="learnFirst"
          id="learn-first"
          placeholder="Javascript"
        />
      </div>
      <div class="form-box">
        <label for="used-languages"
          >Would you like to start learning today?</label
        >
        <div class="form-checkbox">
          <div class="form-option">
            <div
              class="dropdown-btn wants"
              @click="changePos"
              data-option="true"
            ></div>
            <label>Yes</label>
          </div>
          <div class="form-option">
            <div
              class="dropdown-btn doesnt-want"
              @click="changeNeg"
              data-option="false"
            ></div>
            <label>No</label>
          </div>
        </div>
      </div>
    </form>
    <a class="btn-submit" @click="onSubmit" href="#">Submit</a>
  </div>
</template>

<script>
export default {
  name: "TheCant",

  data() {
    return {
      whyNot: "",
      learnFirst: "",
      learnToday: "",
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      const userInfo = {
        whyNot: this.whyNot,
        learnFirst: this.learnFirst,
        learnToday: this.learnToday,
      };
      this.$emit("user-info", userInfo);
    },

    changePos() {
      if (
        document
          .querySelectorAll(".dropdown-btn")[1]
          .classList.contains("check-active")
      ) {
        document
          .querySelectorAll(".dropdown-btn")[1]
          .classList.remove("check-active");
        document
          .querySelectorAll(".dropdown-btn")[0]
          .classList.add("check-active");
        this.learnToday = true;
        return;
      }
      document
        .querySelectorAll(".dropdown-btn")[0]
        .classList.add("check-active");
      this.learnToday = true;
    },

    changeNeg() {
      if (
        document
          .querySelectorAll(".dropdown-btn")[0]
          .classList.contains("check-active")
      ) {
        document
          .querySelectorAll(".dropdown-btn")[0]
          .classList.remove("check-active");
        document
          .querySelectorAll(".dropdown-btn")[1]
          .classList.add("check-active");
        this.learnToday = false;
        return;
      }
      document
        .querySelectorAll(".dropdown-btn")[1]
        .classList.add("check-active");
      this.learnToday = false;
    },
  },
};
</script>
