<template>
  <div class="container-lg">
    <div class="row">
        <div class="col">
            <div class="clock mx-auto d-flex justify-content-center align-items-center">
                <h3 class=" display-3 fw-medium" :class="{'active': start}">{{ hours }}:{{ mins }}:{{ secs }}</h3>
            </div>
        </div>
    </div>
  </div>
</template>

<script setup>
// import { ref } from 'vue';
import { defineProps } from 'vue';

const props = defineProps({
    hours: {
        type: String,
    },
    mins: {
        type: String,
    },
    secs: {
        type: String,
    },
    start: String,
});
</script>
