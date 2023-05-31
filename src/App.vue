<script setup lang="ts">
import Timer from "./components/Timer.vue";
import { ref, onMounted, onUnmounted } from "vue";

const RemainingDays = ref("");
const RemainingHours = ref("");
const RemainingMinutes = ref("");
const RemainingSeconds = ref("");

const newYears = "1 Jan 2024";

function countDown() {
  const newYearsDate: Date = new Date(newYears);
  const currentDate: Date = new Date();

  const totalSeconds = (newYearsDate.getTime() - currentDate.getTime()) / 1000;
  const days = Math.floor(totalSeconds / 3600 / 24);
  const hours = Math.floor(totalSeconds / 3600) % 24;
  const mins = Math.floor(totalSeconds / 60) % 60;
  const seconds = Math.floor(totalSeconds) % 60;

  RemainingDays.value = setTime(days);
  RemainingHours.value = setTime(hours);
  RemainingMinutes.value = setTime(mins);
  RemainingSeconds.value = setTime(seconds);
}

function setTime(value: number) {
  return value >= 10 ? value.toString() : `0${value}`;
}

let timeInterval: ReturnType<typeof setInterval>;

onMounted(() => {
  setInterval(countDown, 1000);
});

onUnmounted(() => {
  clearInterval(timeInterval);
});
</script>

<template>
  <div class="container">
    <div class="title">New Year Countdown</div>
    <div class="subtitle">New beginnings are coming</div>
    <div class="timer">
      <Timer :count="RemainingDays" label="Days" />
      <Timer :count="RemainingHours" label="Hours" />
      <Timer :count="RemainingMinutes" label="Minutes" />
      <Timer :count="RemainingSeconds" label="Seconds" />
    </div>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Tsukimi+Rounded:wght@400;700&display=swap");

body {
  margin: 0;
  font-family: "Tsukimi Rounded", sans-serif;
}

.title {
  max-width: 100%;
  text-align: center;
  font-size: 5rem;
  font-weight: 700;
  color: #b9b4b4;
}

.subtitle {
  position: absolute;
  top: 150px;
  width: 100%;
  text-align: center;
  font-size: 2rem;
  font-weight: bold;
  color: #a19e9e;
}

.container {
  height: 100vh;
  background-image: url("./assets/pexels-eberhard-grossgasteiger-572897.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center center;
  position: relative;
}

.timer {
  max-width: 1280px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: space-around;
}

@media (max-width: 600px) {
  .title {
    font-size: 2rem;
  }
}

@media (max-width: 920px) {
  .title {
    font-size: 3rem;
  }
}

@media (max-width: 320px) {
  .title {
    font-size: 2rem;
  }
}
</style>
