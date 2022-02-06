<template>
  <div class="countdown-timer">
    <span v-if="days">{{ days }}d</span>
    <span v-if="hours">{{ hours }}h</span>
    <span>{{ minutes }}m</span>
    <span>{{ seconds }}s</span>
  </div>
</template>

<script setup>
import { ref } from "vue";


const props = defineProps({
  date: [Date, String, Number],
});

let days = ref();
let hours = ref();
let minutes = ref();
let seconds = ref();

let date = props.date;
if (!(date instanceof Date)) {
  date = new Date(date);
}

setInterval(updateTime, 1000);
updateTime();

function updateTime() {
  // Get Current time
  const currTime = Date.now();
  // Find the different in seconds
  const diff = (date.getTime() - currTime) / 1000;
  // Calculate days
  days.value = Math.floor(diff / (3600 * 24));
  // Calculate the rest of the time
  let remainder = diff % (3600 * 24);
  // Calculate hours
  hours.value = Math.floor(remainder / 3600);
  // Calculate the rest of the time
  remainder = remainder % 3600;
  // Calculate minutes
  minutes.value = Math.floor(remainder / 60);
  // Calculte the rest of the time
  remainder = remainder % 60;
  // Calculte seconds
  seconds.value = Math.floor(remainder);
}
</script>

<style>
.countdown-timer {
  display: flex;
  justify-content: center;
}
.countdown-timer > span {
  padding: 0 0.5rem;
  background-color: #4582d1;
  margin: 0 0.25rem;
  border-radius: 10px;
  color: white
}
</style>
