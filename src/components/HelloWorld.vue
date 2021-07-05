<template>
  <div>
    <span class="timer"
      >Timer : 00:00:<span class="countdown">{{ countDown }}</span></span
    >
    <br />
    <!-- <span class="word">{{ vocabulary }}</span> -->
  </div>
</template>

<script>
import { words } from "../database/words";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data: function () {
    return {
      vocabulary: "",
      countDown: 15,
      question: 3,
    };
  },
  created() {
    // this.vocabulary = words[Math.floor(Math.random() * words.length)];
    this.countDownTimer();
  },
  watch: {
    countDown() {
      if (this.countDown === 0 && this.question > 0) {
        this.countDown = 15;
        this.question -= 1;
        this.vocabulary = words[Math.floor(Math.random() * words.length)];
        this.countDownTimer();
        let music = new Audio(
          "http://www.realmofdarkness.net/audio/vg/sf/sf2/perfect.mp3"
        );
        music.play();
      }
    },
  },
  methods: {
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.timer {
  color: #a30808;
  font-weight: bold;
  font-size: large;
  margin: 0px 108px;
}
</style>
