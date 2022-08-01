<template>
  <div class="form-dropdown-can-code form-dropdown index hidden" id="can-code">
    <div class="dropdown-heading">
      <h2 class="heading-secondary">Tell us more</h2>
      <p class="subheading">Its gonna be quick</p>
    </div>
    <form autocomplete="off" class="dropdown-container">
      <div class="form-box">
        <label for="used-languages">What languages do you use?</label>
        <input
          v-model="usedLangs"
          type="text"
          id="used-languages"
          placeholder="Javascript C# Ruby Perl"
        />
      </div>
      <div class="form-box">
        <label for="favorite-language">Which one is your favorite?</label>
        <input
          type="text"
          v-model="favoriteLang"
          id="favorite-language"
          placeholder="Javascript"
        />
      </div>
      <div class="form-box">
        <label for="question-why">Why did you learn coding?</label>
        <input
          type="text"
          v-model="whyLearn"
          id="question-why"
          placeholder="Its fun"
        />
      </div>
    </form>
    <a class="btn-submit" @click="onSubmit" href="#">Submit</a>
  </div>
</template>

<script>
export default {
  name: "TheCan",
  data() {
    return {
      usedLangs: "",
      favoriteLang: "",
      whyLearn: "",
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      const userInfo = {
        usedLangs: this.usedLangs,
        favoriteLang: this.favoriteLang,
        whyLearn: this.whyLearn,
      };
      this.$emit("user-info", userInfo);
    },
  },
};
</script>
