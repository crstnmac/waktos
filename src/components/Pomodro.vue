<template>
<div>
  <h2 class="title is-6">{{ title }}</h2>

  <q-circular-progress show-value class="text-white q-ma-md" :max="max" :value="minutes" size="200px" :thickness="0.2" color="orange" center-color="grey-8" track-color="transparent">
    {{ minutes }}:{{ seconds }}
  </q-circular-progress>
  <q-btn-group>
    <q-btn id="start" @click="startTimer" :disable="disabled">
      start
    </q-btn>
    <q-btn @click="stopTimer"> stop</q-btn>
    <q-btn @click="resetTimer">reset</q-btn>
  </q-btn-group>
</div>
</template>

<script>
const TIME_LIMIT = 5;

export default {
  data() {
    return {
      max: 25,
      disabled: false,
      timer: null,
      totalTime: 25 * 60,
      resetButton: false,
      title: "Let the countdown begin!!"
    };
  },
  methods: {
    startTimer() {
      this.timer = setInterval(() => this.countdown(), 1000);
      this.resetButton = true;
      this.title = "Greatness is within sight!!";
      this.disabled = true;
    },
    stopTimer() {
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = true;
      this.title = "Never quit, keep going!!";
      this.disabled = false;
    },
    resetTimer() {
      this.totalTime = 25 * 60;
      clearInterval(this.timer);
      this.timer = null;
      this.resetButton = false;
      this.title = "Let the countdown begin!!";
      this.disabled = false;
    },
    padTime(time) {
      return (time < 10 ? "0" : "") + time;
    },
    countdown() {
      this.totalTime--;
    }
  },
  computed: {
    minutes: function () {
      const minutes = Math.floor(this.totalTime / 60);
      return this.padTime(minutes);
    },
    seconds: function () {
      const seconds = this.totalTime - this.minutes * 60;
      return this.padTime(seconds);
    }
  }
};
</script>
