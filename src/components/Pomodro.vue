<template>
<div>
  <h2 class="title is-6">{{ title }}</h2>

  <q-circular-progress show-value class="text-white q-ma-md" v-model="timeLimit" :max="timeLimit" :value="Number(minutes)" size="200px" :thickness="0.2" color="orange" center-color="grey-8" track-color="transparent">
    {{ minutes }}:{{ seconds }}
  </q-circular-progress>

  <div class="q-pa-md">
    <q-badge color="secondary"> Model: {{ timeLimit }} (0 to 25) </q-badge>

    <q-slider @change="getTime" v-model="timeLimit" :min="0" :max="25" />
  </div>

  <q-btn-group>
    <q-btn @click="startTimer" :disable="disabled">
      start
    </q-btn>
    <q-btn @click="stopTimer"> stop</q-btn>
    <q-btn @click="resetTimer">reset</q-btn>
  </q-btn-group>
</div>
</template>

<script>
export default {
  data() {
    return {
      timeLimit: 25,
      totalTime: 25 * 60,
      disabled: false,
      timer: null,
      resetButton: false,
      title: "Let the countdown begin!!"
    };
  },

  methods: {
    getTime() {
      this.minutes;
      this.seconds;
      this.totalTime = this.timeLimit * 60;
    },
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
      this.totalTime = this.timeLimit * 60;
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
      console.log(this.totalTime);
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
