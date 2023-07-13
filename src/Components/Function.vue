<template>
<div class="container-lg">
    <div class="row">
        <div class="col d-flex justify-content-evenly px-5">
            <button class="btn bg-info d-flex justify-content-center align-items-center" :class="{'disabled': start}" @click="startTimer">
                <i class="bi bi-play-fill text-primary fs-1"></i>
            </button>
            <button class="btn bg-info d-flex justify-content-center align-items-center" :class="{'disabled': !start}" @click="pauseTimer">
                <i class="bi bi-pause-fill text-primary fs-1"></i>
            </button>
            <button class="btn bg-info d-flex justify-content-center align-items-center" @click="add10secs">
                <i class="bi bi-plus-circle-fill text-primary fs-2"></i>
            </button>
        </div>
    </div>
</div>  
</template>

<script setup>
const props = defineProps(['start']);

const emit = defineEmits(['startTimer', 'pauseTimer', 'add10secs']);

const add10secs = () => {
    emit('add10secs');
};

const startTimer = () => {
    emit('startTimer');
};

const pauseTimer = () => {
    emit('pauseTimer');
}

</script>
