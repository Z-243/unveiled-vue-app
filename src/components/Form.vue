<script setup>
import { ref } from "vue";

const { handleCloseModal, handleUpdateData } = defineProps({
  handleCloseModal: Function,
  handleUpdateData: Function,
});

const name = ref("");
const day = ref(1);
const month = ref(1);
const currYear = new Date().getFullYear();
const year = ref(currYear);
const lifeExpectancy = ref(90);

// Options
// create a days array from 1-31
const days = Array.from({ length: 31 }, (_, i) => i + 1);
const months = [
  "January",
  "February",
  "March",
  "April",
  "May",
  "June",
  "July",
  "August",
  "September",
  "October",
  "November",
  "December",
];
// create an years array from currYear(2025) to -99(1926)
const years = Array.from({ length: 100 }, (_, i) => currYear - i);

function handleSave() {
  handleUpdateData(
    // Sam, 1996-11-23, 90 format
    name.value,
    `${year.value}-${month.value}-${day.value}`,
    lifeExpectancy.value
  );
}
</script>

<template>
  <section id="form">
    <div>
      <h4 class="text-gradient">Your Details</h4>
      <button @click="handleCloseModal" class="link-button">
        <i class="fa-regular fa-circle-xmark"></i>
      </button>
    </div>
    <div>
      <label for="name">Name</label>
      <!-- value, onChange in react; v-model/ :value & @input in vue -->
      <input v-model="name" type="text" id="name" required />
    </div>
    <div>
      <div>BirthDay</div>
      <div class="bday">
        <select v-model="day">
          <option v-for="d in days" :key="d" :value="d">{{ d }}</option>
        </select>
        <select v-model="month">
          <option
            v-for="(m, mIndex) in months"
            :key="mIndex"
            :value="mIndex + 1"
          >
            {{ m }}
          </option>
        </select>
        <select v-model="year">
          <option v-for="y in years" :key="y" :value="y">{{ y }}</option>
        </select>
      </div>
    </div>
    <div>
      <label for="lifeExpectancy">Life Expectancy (years)</label>
      <input
        id="lifeExpectancy"
        type="number"
        max="120"
        required
        v-model="lifeExpectancy"
      />
    </div>
    <button @click="handleSave">Submit</button>
  </section>
</template>

<style scoped></style>
