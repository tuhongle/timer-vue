<template>
  <div class="container-lg">
    <div class="row">
        <div class="col">
            <div class="clock mx-auto d-flex justify-content-center align-items-center position-relative">
                <h3 class=" display-3 fw-medium" :class="{'active': start}">{{ hours }}:{{ mins }}:{{ secs }}</h3>
                <button v-if="!muted" class="btn position-absolute bottom-0 shadow-none border-0" @click="mute">
                    <i class="bi bi-megaphone-fill fs-1 text-primary"></i>
                </button>
                <button v-else class="btn position-absolute bottom-0 shadow-none border-0" @click="unmute">
                    <i class="bi bi-mic-mute-fill fs-1 opacity-50 text-primary"></i>
                </button>
            </div>
        </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

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
    start: Boolean,
});

const muted = ref(false);

const emit = defineEmits(['mute', 'unmute']);

const mute = () => {
    emit('mute');
    muted.value = true;
};

const unmute = () => {
    emit('unmute');
    muted.value = false;
}
</script>
