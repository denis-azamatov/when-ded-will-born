<template>
  <div class="timer">
    <Countdown v-if="date" :date="date"></Countdown>
    <div v-else>
      <div>
        <img loading="lazy" class="gif1" src="https://s3.eu-central-1.amazonaws.com/ded.gifs/gif1.gif" alt="">
        <img loading="lazy" class="gif2" src="https://s3.eu-central-1.amazonaws.com/ded.gifs/gif2.gif" alt="">
        <img loading="lazy" class="gif3" src="https://s3.eu-central-1.amazonaws.com/ded.gifs/gif3.gif" alt="">
        <img loading="lazy" class="gif4" src="https://s3.eu-central-1.amazonaws.com/ded.gifs/gif4.gif" alt="">
        <img loading="lazy" class="gif5" src="https://s3.eu-central-1.amazonaws.com/ded.gifs/gif5.gif" alt="">
        <img loading="lazy" class="gif7" src="https://s3.eu-central-1.amazonaws.com/ded.gifs/gif7.webp" alt="">
        <img loading="lazy" class="gif6" src="https://s3.eu-central-1.amazonaws.com/ded.gifs/gif6.gif" alt="">
      </div>
      <div class="title">
        <p>
          Happy birthday DED!
        </p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import Countdown from './components/Countdown.vue';

function compareDate(first: Date, secondDate: Date): boolean {
  return first.getFullYear() == secondDate.getFullYear()
    && first.getDate() == secondDate.getDate()
    && first.getMonth() == secondDate.getMonth();
}

/**
 * Returns next bday or null if it is today
 */
function getNext() {
  const now = new Date(2023, 10, 26);
  const currentYear = now.getFullYear();

  let target = new Date(currentYear, 10, 26);

  if (target > now) {
    return target;
  }

  if (compareDate(now, target)) {
    return null;
  }

  return new Date(currentYear + 1, 10, 26);
}

const date = getNext();
</script>


<style scoped>
.title {
  z-index: 2;
  position: relative;
}

.title p {
  font-size: 6rem;
  animation: blink 1s steps(2, start) infinite;
}

@keyframes blink {
  0% {
    opacity: 0;
  }

  100% {
    opacity: 1;
  }
}

img {
  position: absolute;
  z-index: 1;
}

.gif1 {
  top: 5rem;
}

.gif2 {
  top: 15rem;
  left: 5rem
}

.gif3 {
  bottom: 3rem;
  right: 5rem
}

.gif4 {
  bottom: 2rem;
  right: 50rem;
}

.gif5 {
  top: 2rem;
  right: 2rem;
}

.gif6 {
  bottom: 2rem;
  right: 35rem;
}

.gif7 {
  top: 2rem;
  left: 10rem;
}

@media screen and (max-width: 768px) {


  .gif1 {
    z-index: 10;
  }

  .gif7 {
    top: unset;
    bottom: 2rem;
    left: 0rem;
    width: 100%;
  }
}
</style>
