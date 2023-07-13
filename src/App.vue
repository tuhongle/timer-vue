<template>
  <main class="content-wrapper mx-auto py-5">
    <h1 class="display-3 fw-bold text-center text-primary mb-4">Timer App</h1>
    <section class="clockComp">
      <Clock :hours="hours" :mins="mins" :secs="secs" :start="start"/>
    </section>
    <section class="funcComp mt-4">
      <Function @add10secs="add10secs" @startTimer="startTimer" @pauseTimer="pauseTimer" :start="start" />
    </section>
    <section class="setTime mt-4">
      <SetTime @set1hour="set1hour" @set30min="set30min" @set15min="set15min" @setTime="setTime" :start="start" />
    </section>
  </main>
</template>

<script setup>
import { ref } from "vue";
import Clock from "./Components/Clock.vue";
import Function from "./Components/Function.vue";
import SetTime from "./Components/SetTime.vue";

const hours = ref('00');
const mins = ref('00');
const secs = ref('00');
const start = ref(false);
const paused = ref(false);

/* const time = computed(() => {
  return ~~(hours.value) * 3600 + ~~(mins.value) * 60 + ~~(secs.value);
}); */

const set1hour = () => {
  hours.value = '01';
  mins.value = '00';
  secs.value = '00';
};

const set30min = () => {
  hours.value = '00';
  mins.value = '30';
  secs.value = '00';
};

const set15min = () => {
  hours.value = '00';
  mins.value = '15';
  secs.value = '00';
};

const setTime = data => {
  const time = data.split(':');
  hours.value = time[0];
  mins.value = time[1];
  secs.value = time[2];
}

const timerFunc = (num) => {
  hours.value = Math.floor(num / 3600).toString();
  mins.value = Math.floor((num - ~~hours.value * 3600) / 60).toString();
  secs.value = Math.floor((num - ~~hours.value * 3600 - ~~mins.value * 60)).toString();
  if (hours.value.length === 1) {
    hours.value = '0' + hours.value;
  };
  if (mins.value.length === 1) {
    mins.value = '0' + mins.value;
  };
  if (~~secs.value < 10) {
    secs.value = '0' + secs.value;
  };
};

const add10secs = () => {
  const times = ~~hours.value * 3600 + ~~mins.value * 60 + ~~secs.value + 10;
  // const times = time.value + 10;
  timerFunc(times);
};

const startTimer = () => {
  if (hours.value !== '00' || mins.value !== '00' || secs.value !== '00') {
    start.value = true;
    paused.value = false;
  };
  setInterval(() => {
    if (!(paused.value)) {
      let times = ~~hours.value * 3600 + ~~mins.value * 60 + ~~secs.value;
      if (times > 1) {
        times --;
        timerFunc(times);
        console.log(times);
      } else {
        times --;
        timerFunc(times);
        paused.value = true;
        start.value = false;
      }
    }
  }, 1000);
};

const pauseTimer = () => {
  paused.value = true;
  start.value = false;
};

</script>

