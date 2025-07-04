<script setup>
import { ref } from "vue";
import Calendar from "./components/Calendar.vue";
import Clocks from "./components/Clocks.vue";
import Hero from "./components/Hero.vue";
import Layout from "./components/layouts/Layout.vue";
import Summary from "./components/Summary.vue";
import { calculateTimeLeft, getLifePercentageLived } from "./utils";
import Portal from "./components/Portal.vue";
import Form from "./components/Form.vue";
import { computed } from "vue";
import { onMounted } from "vue";
import { watchEffect } from "vue";

const defaultBD = "1996-11-23";
const defaultLE = 90;

// use ref to declare stateful variables/references
const birthDate = ref(defaultBD);
const lifeExpectancy = ref(defaultLE);
const name = ref("Sam");
// ref can't have stateful(ref) values eg birthDate
const data = ref(calculateTimeLeft(defaultBD, defaultLE));

let percentage = computed(() =>
  getLifePercentageLived(birthDate.value, lifeExpectancy.value)
);

const showModal = ref(false);
function handleToggleModal() {
  showModal.value = !showModal.value;
}

function handleUpdateData(n, b, e) {
  if (!n || !b || !e) {
    return;
  }

  // save new data to localStorage
  localStorage.setItem(
    "formData",
    JSON.stringify({
      name: n,
      birthDate: b,
      lifeExpectancy: e,
    })
  );

  name.value = n;
  birthDate.value = b;
  lifeExpectancy.value = parseInt(e);
  data.value = calculateTimeLeft(b, parseInt(e));
  showModal.value = false;
}

function resetData() {
  name.value = "Sam";
  birthDate.value = defaultBD;
  lifeExpectancy.value = defaultLE;
  data.value = calculateTimeLeft(defaultBD, defaultLE);
  localStorage.clear();
}

const totalProps = {
  birthDate,
  lifeExpectancy,
  name,
  data,
  percentage,
};

// life-cycle hook/ onMounted – executed when page loads
onMounted(() => {
  if (!localStorage) {
    return;
  }
  if (localStorage.getItem("formData")) {
    //name:n – to not cause naming conflict and these variables already exist
    const {
      name: n,
      birthDate: b,
      lifeExpectancy: e,
    } = JSON.parse(localStorage.getItem("formData"));

    name.value = n;
    birthDate.value = b;
    lifeExpectancy.value = parseInt(e);
    data.value = calculateTimeLeft(b, parseInt(e));
  }
});

// watchEffect re-executed the cleanup runs
// could have also use unMounted with this
// when ever the ref(birthDate) changes code is re-run
watchEffect((onCleanup) => {
  const interval = setInterval(() => {
    // every 1000ms/1 sec recalculate time left
    data.value = calculateTimeLeft(birthDate.value, lifeExpectancy.value);
  }, 1000);

  onCleanup(() => clearInterval(interval));
});
</script>

<template>
  <Layout>
    <Portal :handleCloseModal="handleToggleModal" :showModal="showModal">
      <Form
        :handleCloseModal="handleToggleModal"
        :handleUpdateData="handleUpdateData"
      />
    </Portal>
    <!-- :name(to destructure)=name(variable name) for dynamic values -->
    <!-- name="Sam" for static values – this works -->
    <Hero
      :name="name"
      :data="data"
      :handleToggleModal="handleToggleModal"
      :percentage="percentage"
      :resetData="resetData"
    />
    <Clocks v-bind="totalProps" />
    <Calendar v-bind="totalProps" />
    <Summary v-bind="totalProps" />
  </Layout>
</template>

<style scoped></style>
