<template>
  <BubbleAnimation/>
  <div class="content">
    <CountDown
        v-bind:current-time="currentTime"
        v-bind:count-down-to="countDownTo"
    />
    <BoatSimulator
        v-bind:current-time="currentTime"
        v-bind:count-down-from="countDownFrom"
        v-bind:count-down-to="countDownTo"
    />
  </div>
</template>

<script>
import CountDown from "@/components/CountDown.vue";
import BoatSimulator from "@/components/BoatSimulator.vue";
import BubbleAnimation from "@/components/BubbleAnimation.vue";

export default {
  name: 'App',
  components: {BubbleAnimation, BoatSimulator, CountDown},
  data() {
    return {
      currentTime: new Date(),
      countDownFrom: new Date(2023, 7, 17, 0, 0),
      countDownTo: new Date(2023, 7, 25, 18, 30),
    }
  },
  created() {
    this.startCurrentTimeTick();
  },

  methods: {
    startCurrentTimeTick() {
      setInterval(() => {
        this.currentTime = new Date();
      }, 1000)
    }
  }
}
</script>

<style>
html, body, #app {
  height: 100%;
  margin: unset;
  padding: unset;
  background-color: #29b6f6;
}
</style>

<style scoped>
.content {
  position: relative;
  display: flex;
  flex-direction: column;
  padding: 2rem 2rem 0 2rem;
  background-color: #29b6f6;
  border-bottom: solid 2px #0182b0;
}
</style>