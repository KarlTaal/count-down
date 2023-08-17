<template>
  <div style="overflow-x: auto">
    <div class="boat-container">
      <div class="boat-start">
        <img src="../assets/images/start-flag.png" alt="Start flag image"/>
      </div>
      <div class="boat-overlay-container">
        <div class="boat">
          <img src="../assets/images/tallink-ship.png" alt="Ship image"/>
        </div>
      </div>
      <div class="boat-finish">
        <img src="../assets/images/finish-flag.png" alt="Finish flag image"/>
      </div>
    </div>
  </div>

</template>


<script>

export default {
  name: "boat-simulator",
  props: {
    currentTime: {
      type: Date,
      required: true
    },
    countDownFrom: {
      type: Date,
      required: true
    },
    countDownTo: {
      type: Date,
      required: true
    },
  },
  computed: {
    marginPercentageDoneFromStartToEnd() {
      const timeDoneSoFar = Math.max(0, this.currentTime.getTime() - this.countDownFrom.getTime());
      const totalTimeFromStartToEnd = Math.max(0, this.countDownTo.getTime() - this.countDownFrom.getTime());
      return `${ Math.min(100, timeDoneSoFar / totalTimeFromStartToEnd * 100) }%`;
    }
  }
}


</script>

<style lang="scss" scoped>
$boat-width: 15vw;
$boat-height: 6vw;
$flag-size: 4vw;

.boat-container {
  position: relative;
  display: flex;
  align-items: end;
  justify-content: space-between;
  min-width: calc(4 * $boat-width);
  height: $boat-height;
  overflow-y: hidden;
}

.boat-start, .boat-finish {
  width: $flag-size;
  height: $flag-size;
  img {
    width: $flag-size;
    height: $flag-size;
  }
}

.boat-start {
  margin-left: calc($boat-width);
}

.boat-finish {
  margin-right: calc($boat-width);
}

.boat-overlay-container {
  z-index: 5;
  position: absolute;
  top: 0;
  left: 0;
  width: calc(100% - $boat-width);
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;

  .boat {
    display: flex;
    flex-direction: column;
    justify-content: end;
    height: 100%;
    width: $boat-width;
    margin-left: v-bind(marginPercentageDoneFromStartToEnd);

    img {
      width: $boat-width;
      max-height: $boat-height;
      height: $boat-height;
    }
  }
}
</style>