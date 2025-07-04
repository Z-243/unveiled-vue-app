<script setup>
import { getTimePercentage } from "../utils";

defineProps({
  data: Object,
});

let snapshot = getTimePercentage();
</script>

<template>
  <section id="clocks">
    <p><i>Your remaining time in different measuring units.</i></p>
    <div class="clocks-grid">
      <!-- v-for – create an array of keys(years,hours) -->
      <!-- create cards for each key(here 7) -->
      <div
        class="card clock-card"
        v-for="(clock, clockIndex) in Object.keys(data.value)"
        :key="clockIndex"
      >
        <!-- create a circle; rotate it acc to time percentage and deg(degree) -->
        <!-- how much should the circle rotate to show time spent/left -->
        <div class="circle" :style="{ rotate: snapshot[clock] + 'deg' }">
          <!-- give ticker :class - years,hours,etc which can be set as true or false-->
          <!-- after how much time should the ticker move -->
          <div class="ticker" :class="{ [clock]: true }"></div>
        </div>
        <div>
          <!-- get values of different clock keys – years, hours, etc -->
          <h5 class="text-h5-like">{{ data.value[clock] }}</h5>
          <p>{{ clock }}</p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
