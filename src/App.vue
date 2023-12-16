<script setup lang="ts">
import { ref } from "vue";
import useDate from "./composables/useDate";

const daysToAdd = ref(0);
const monthsToAdd = ref(0);
const heading = ref("Current Date");

const { date, getDay, getMonth, getYear, addDay, addMonth } = useDate();
const dates = ref(date.toString());

const handleInputChange = (event: Event) => {
  let { name, value } = event.target as HTMLInputElement;
  if (name === "day") {
    if (!value) value = "0";
    daysToAdd.value = parseInt(value);
  } else if (name === "month") {
    if (!value) value = "0";
    monthsToAdd.value = parseInt(value);
  }
};

const handleAddDaysAndMonths = () => {
  const newDate = addMonth(monthsToAdd.value, addDay(daysToAdd.value, date));
  return newDate;
};

const handleClick = () => {
  heading.value = "Updated date:";
  dates.value = handleAddDaysAndMonths().toString();
};
</script>

<template>
  <div class="container">
    <h2>Today</h2>
    {{ getDay() }}, {{ getMonth() }} {{ getYear() }}.
    <br />
    <h2>{{ heading }}</h2>
    <p>Date: {{ dates }}</p>
    <br />
    Add Day: <input name="day" type="number" @change="handleInputChange" />
    <br />
    Add Month: <input name="month" type="number" @change="handleInputChange" />
    <br />
    <button class="btn" @click="handleClick">Change The World</button>
  </div>
</template>

<style scoped></style>
