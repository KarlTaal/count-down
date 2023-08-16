<template>
  <h1>Time until no more Tallink!</h1>
  <p>{{ counterValue }}</p>
</template>


<script>


export default {
  name: "count-down",
  props: {
    currentTime: {
      type: Date,
      required: true
    },
    countDownTo: {
      type: Date,
      required: true
    },
  },
  computed: {
    counterValue() {
      const secondsFromCurrentTimeToEnd = Math.max(0, (this.countDownTo.getTime() - this.currentTime.getTime()) / 1000);
      const hours = Math.floor(secondsFromCurrentTimeToEnd / 3600);
      const minutes = Math.floor((secondsFromCurrentTimeToEnd - (hours * 3600)) / 60);
      const seconds = Math.floor((secondsFromCurrentTimeToEnd - (hours * 3600)) - (minutes * 60));
      return `${ hours.toString().padStart(2, '0') }:${ minutes.toString().padStart(2, '0') }:${ seconds.toString().padStart(2, '0') }`;
    }
  }
}


</script>

<style scoped>
* {
  text-align: center;
}

p {
  font-weight: bold;
  font-size: 2rem;
  z-index: 100;
}
</style>