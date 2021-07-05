<template>
  <div>
    <button v-if="!showTest" @click="startTest()">Start Test</button>
    <div v-if="showTest">
      <div v-if="question > 0">
        <span class="timer"
          >Timer : 00:00:<span class="countdown">{{ countDown }}</span></span
        >
        <br />
        <br /><br />
        <span class="word">{{ 60 - question + 1 }}) {{ vocabulary }}</span>
      </div>
      <div v-else class="timer">End :)</div>
    </div>
  </div>
</template>
<script>
import { words } from "./database/words";
export default {
  name: "App",
  data: function () {
    return {
      vocabulary: "",
      countDown: 15,
      question: 60,
      showTest: false,
    };
  },
  created() {},
  watch: {
    countDown() {
      if (this.countDown === 0 && this.question > 0) {
        let music = new Audio(
          "http://www.realmofdarkness.net/audio/vg/sf/sf2/perfect.mp3"
        );
        music.play();
        this.countDown = 15;
        this.question -= 1;
        this.vocabulary = words[Math.floor(Math.random() * words.length)];
        this.countDownTimer();
      }
    },
  },
  methods: {
    startTest() {
      this.showTest = true;
      this.vocabulary = words[Math.floor(Math.random() * words.length)];
      this.countDownTimer();
    },
    countDownTimer() {
      if (this.countDown > 0) {
        setTimeout(() => {
          this.countDown -= 1;
          this.countDownTimer();
        }, 1000);
      }
    },
  },
};
</script>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.timer {
  color: #a30808;
  font-weight: bold;
  font-size: large;
  margin: 0px 108px;
}
.word {
  font-weight: bold;
  font-size: x-large;
}
</style>
