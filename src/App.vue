<template>
  <main class="content-wrapper mx-auto py-5">
    <h1 class="display-3 fw-bold text-center text-primary mb-4">Timer App</h1>
    <section class="clockComp">
      <Clock :hours="hours" :mins="mins" :secs="secs" :start="start" @mute="muteSound" @unmute="unmuteSound"/>
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

import oneSecond from './assets/onesecond.mp3';
import timerEnding from './assets/timerending.mp3';

const hours = ref('00');
const mins = ref('00');
const secs = ref('00');

let start = ref(false);

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

let timerInterval;
let audioInterval;

const audio = new Audio(oneSecond);
const timer = new Audio(timerEnding);

const startTimer = () => {
  if (hours.value !== '00' || mins.value !== '00' || secs.value !== '00') {
    start.value = true;
    timerInterval = setInterval(() => {
      let times = ~~hours.value * 3600 + ~~mins.value * 60 + ~~secs.value;
      if (times > 1) {
        times --;
        timerFunc(times);
        if (times === 1) {
          clearInterval(audioInterval);
        };
      } else {
        times --;
        timerFunc(times);
        start.value = false;
        clearInterval(timerInterval);
        timer.play();
        if (timer.muted) {
          setTimeout(() => {
            alert('Time is up')
          }, 200);
        }
      }
    }, 1000);
    setTimeout(() => {
      audioInterval = setInterval(() => {
        audio.play();
      },0);
    },300);
  };
};

const pauseTimer = () => {
  clearInterval(timerInterval);
  clearInterval(audioInterval);
  start.value = false;
};

const muteSound = () => {
  audio.muted = true;
  timer.muted = true;
};

const unmuteSound = () => {
  audio.muted = false;
  timer.muted = false;
}

</script>

