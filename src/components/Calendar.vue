<script setup>
import { computed } from "vue";

const { data, lifeExpectancy } = defineProps({
  data: Object,
  lifeExpectancy: Object,
});

// computed vaalues – change when stateful variables change – here lifeExpectancy
// create lifeExpectancy array from 0-89
const yearsArr = computed(() => [...Array(lifeExpectancy.value).keys()]);
// create array from 0-51
const weeksArr = [...Array(52).keys()];

// weeks spent = total weeks - weeks left
const weekNum = computed(
  () => lifeExpectancy.value * 52 - parseInt(data.value["weeks"])
);

const finalWeek = computed(() => lifeExpectancy.value * 52);

function getWeekArr(wksArr, yrIndex) {
  // for every week
  return wksArr.map((val, valIndex) => {
    // yrIndex 0-89; valIndex 0-51 – helps iterates over every week in a year
    const currWeek = yrIndex * 52 + valIndex;

    // are we in the final week
    // computed values need to be accessed using .value otherwise it gives us reference
    const dotStyle =
      currWeek == finalWeek.value - 1
        ? " death"
        : // week has been spent
        currWeek < weekNum.value
        ? " solid"
        : // in the present week
        currWeek == weekNum.value
        ? " pulse"
        : "";
    // reutrns week 0-51: 0-51, currWeek being itertated, dotStyle associated with it
    return { week: val, currWeek, dotStyle };
  });
}
</script>

<template>
  <section id="calendar">
    <p>
      <i>Each square of dots represents 1 year / 52 weeks of your life.</i>
    </p>
    <div class="dozen-grid">
      <!-- contains each year expected to live -->
      <div
        class="year-grid"
        v-for="(year, yearIndex) in yearsArr"
        :key="yearIndex"
      >
        <!-- create dots of 52 weeks for each year -->
        <!-- give dynamic class to each dot/week -->
        <div
          v-for="(week, weekIndex) in getWeekArr(weeksArr, yearIndex)"
          :key="weekIndex"
          :class="week.dotStyle"
          class="dot"
        ></div>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
