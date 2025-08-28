<script setup>
// destructure props – 2 ways

// 1st way – these props are accessable only in <template> not in <script>
// defineProps({
//     name: String,
//     data: Object
// })

// 2nd way - make props accessable in <script> also
const { name, data, handleToggleModal, percentage, resetData } = defineProps({
  name: String,
  data: Object,
  handleToggleModal: Function,
  percentage: {
    type: [Object, String],
  },
  resetData: Function,
});

function copyLink() {
  navigator.clipboard.writeText("https://unveiled-time.netlify.app/");
  alert("Link Copied");
}
</script>

<template>
  <section id="hero">
    <h3 class="text-large">
      {{ name }}, you’ve got {{ data["weeks"] }} weeks ahead of you. Get going..
    </h3>
    <div class="btns-container">
      <button @click="handleToggleModal">Not {{ name }}?</button>
      <button @click="copyLink" class="link-button">Copy link</button>
      <button @click="resetData" class="link-button">Reset data</button>
    </div>

    <!-- whole progress bar -->
    <div class="progress-bar">
      <!-- filled bar; :style="{ width: `45%` }" –dynamic style -->
      <div :style="{ width: percentage }">
        <!-- text/icons -->
        <div>
          <i class="fa-solid fa-child-reaching"></i>
          <h6 class="bar-label">Birth</h6>
        </div>
        <h6>{{ percentage }}</h6>
      </div>
      <div>
        <h6 class="bar-label">Death</h6>
        <i class="fa-solid fa-ghost"></i>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
