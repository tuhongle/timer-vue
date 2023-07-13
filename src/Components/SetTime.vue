<template>
    <div class="container-lg">
        <div class="row">
            <div class="col">
                <div class="row">
                    <div class="col-4">
                        <button class="btn btn-cyan text-white w-100 py-3 rounded-4 fs-5" :class="{'disabled': start}" @click="set1hour">1h</button>
                    </div>
                    <div class="col-4">
                        <button class="btn btn-cyan text-white w-100 py-3 rounded-4 fs-5" :class="{'disabled': start}" @click="set30min">30min</button>
                    </div>
                    <div class="col-4">
                        <button class="btn btn-cyan text-white w-100 py-3 rounded-4 fs-5" :class="{'disabled': start}" @click="set15min">15min</button>
                    </div>
                </div>
                <div class="row mt-3">
                    <input type="time" step="1" class="form-control w-100 bg-white border-0 shadow-none py-3 px-3" v-model="timer">
                </div>
                <div class="row mt-3">
                    <button class="btn btn-cyan text-white w-100 py-3 rounded-4 fs-4" :class="{'disabled': start}" @click="setTime">Set custom time</button>
                </div>
            </div>
        </div>
    </div>  
</template>
    
<script setup>
import { ref } from 'vue';
const props = defineProps(['start']);

const emit = defineEmits(['set1hour', 'set30min', 'set15min', 'setTime']);

const timer = ref('00:00:00');

const set1hour = () => {
    emit('set1hour',);
};
const set30min = () => {
    emit('set30min');
};
const set15min = () => {
    emit('set15min');
};
const setTime = () => {
    emit('setTime', timer.value);
}

</script>