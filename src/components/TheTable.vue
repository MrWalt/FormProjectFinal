<template>
  <section class="section-table hidden">
    <div class="container">
      <div class="table">
        <div>
          <label>First Name</label>
          <p class="first-name-sent">{{ sendingData.firstName }}</p>
        </div>
        <div>
          <label>Last Name</label>
          <p class="last-name-sent">{{ sendingData.lastName }}</p>
        </div>
        <div>
          <label>Email Address</label>
          <p class="email-sent">{{ sendingData.email }}</p>
        </div>
        <div v-if="sendingData.job">
          <label>Current Job</label>
          <p class="job-sent">{{ sendingData.job }}</p>
        </div>
        <div>
          <label>Can you code?</label>
          <p class="can-code-sent">{{ sendingData.code }}</p>
        </div>
        <div v-if="sendingData.code === 'Yes' && sendingData.usedLangs">
          <label>What languages do you use?</label>
          <p class="used-langs-sent">{{ sendingData.usedLangs }}</p>
        </div>
        <div v-if="sendingData.code === 'Yes' && sendingData.favoriteLang">
          <label>Which one is your favorite?</label>
          <p class="fav-lang-sent">{{ sendingData.favoriteLang }}</p>
        </div>
        <div v-if="sendingData.code === 'Yes' && sendingData.whyLearn">
          <label>Why did you learn coding?</label>
          <p class="why-learn-sent">{{ sendingData.whyLearn }}</p>
        </div>
        <div v-if="sendingData.code === 'No' && sendingData.whyNot">
          <label>Why not?</label>
          <p class="why-not-sent">{{ sendingData.whyNot }}</p>
        </div>
        <div v-if="sendingData.code === 'No' && sendingData.learnFirst">
          <label>What language would you learn first?</label>
          <p class="learn-first-sent">{{ sendingData.learnFirst }}</p>
        </div>
        <div v-if="sendingData.code === 'No' && sendingData.learnToday">
          <label>Would you like to start learning today?</label>
          <p class="learn-today-sent">{{ sendingData.learnToday }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: "TheTable",
  props: {
    sendingData: Object,
  },
};
</script>
