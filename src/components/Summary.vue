<script setup>
import { computed } from "vue";

const { birthDate, lifeExpectancy } = defineProps({
  birthDate: Object,
  lifeExpectancy: Object,
});

const finalYear = computed(() => {
  const yr = parseInt(birthDate.value.split("-")[0]);
  return yr + lifeExpectancy.value;
});
</script>

<template>
  <section id="summary">
    <div>
      <p class="text-gradient">
        <i class="fa-solid fa-shield-heart"> </i>
        You&apos;ll probably die in the year <strong>{{ finalYear }}</strong> at
        the age of <strong>{{ lifeExpectancy }}</strong
        >.
      </p>
    </div>
    <h4>
      “You can’t go back and change the beginning, but you can start
      <br />
      where you are and change the ending.”
    </h4>
    <h4>C.S. Lewis</h4>
  </section>
</template>

<style scoped></style>
