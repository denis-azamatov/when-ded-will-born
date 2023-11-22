<template>
    <div class="digit">
        BIRTHDAY
    </div>
    <div class="digit">
        SCHEDULED
    </div>
    <div class="block">
        <div>
            <p class="digit">{{ format(days) }}</p>
            <p class="label">Days</p>
        </div>
        <div>
            <p class="digit">{{ format(hours) }}</p>
            <p class="label">Hours</p>
        </div>
        <div>
            <p class="digit">{{ format(minutes) }}</p>
            <p class="label">Minutes</p>
        </div>
        <div>
            <p class="digit">{{ format(seconds) }}</p>
            <p class="label">Seconds</p>
        </div>
    </div>
</template>

<script setup lang="ts">
import { computed, onBeforeUnmount, ref } from 'vue';

const props = defineProps({
    date: {
        type: Date,
        required: true
    }
});

const now = ref(Math.trunc((new Date()).getTime() / 1000));
const target = Math.trunc(props.date.getTime() / 1000);

const interval = window.setInterval(() => {
    now.value = Math.trunc((new Date()).getTime() / 1000);
}, 1000);

const seconds = computed(() => (target - now.value) % 60);
const minutes = computed(() => Math.trunc(((target - now.value) / 60) % 60));
const hours = computed(() => Math.trunc(((target - now.value) / 60 / 60) % 24));
const days = computed(() => Math.trunc((target - now.value) / 60 / 60 / 24));

function format(value: number) {
    if (value.toString().length <= 1) {
        return "0" + value.toString();
    }
    return value.toString();
}

onBeforeUnmount(() => {
    clearInterval(interval);
})
</script>

<style scoped>
.block {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    gap: 1rem;
}

.digit {
    font-size: 6rem;
    white-space: pre;
    margin: 0;
}

.label {
    margin: 0;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    font-size: 2rem;
    color: white;
    text-transform: uppercase;
}

@media screen and (max-width: 768px) {
    .digit {
        font-size: 4rem;
    }

    .label {
        font-size: 1.5rem;
    }
}

@media screen and (max-width: 520px) {
    .digit {
        font-size: 3rem;
    }

    .label {
        font-size: 1rem;
    }
}
</style>