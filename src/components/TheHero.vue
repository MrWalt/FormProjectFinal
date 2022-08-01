<template>
  <section class="section-hero">
    <div class="container">
      <div class="hero">
        <div class="hero-text-box">
          <h1 class="hero-text">Can you code?</h1>
          <a href="#" @click="goToForm" class="btn-hero">Tell us why</a>
        </div>
        <img
          class="hero-img"
          src="../assets/coding.jpg"
          alt="HTML and CSS Coding"
        />
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "TheHero",
  methods: {
    goToForm() {
      document.querySelector(".form-container").classList.remove("hidden");
      setTimeout(function () {
        document.querySelector(".form-container").classList.add("pop-active");
      }, 50);
      setTimeout(function () {
        document
          .querySelector("#section-form")
          .scrollIntoView({ behavior: "smooth" });
      }, 200);
    },
  },
};
</script>
