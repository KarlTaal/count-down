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
$boat-width: 17rem;
$boat-height: 6rem;
$flag-size: 2.5rem;

$boat-sm-width: 10rem;
$boat-sm-height: 4rem;
$flag-sm-size: 2rem;

$boat-xsm-width: 7rem;
$boat-xsm-height: 3rem;
$flag-xsm-size: 1.5rem;


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
  img {
    width: $flag-size;
    height: $flag-size;
    transform: translateY(0.5rem);
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

@media all and (max-width: 1200px) { //smaller than 1200px
  .boat-container {
    min-width: calc(4 * $boat-sm-width);
    height: $boat-sm-height;
  }

  .boat-start, .boat-finish {
    img {
      width: $flag-sm-size;
      height: $flag-sm-size;
    }
  }
  .boat-start {
    margin-left: calc($boat-sm-width);
  }

  .boat-finish {
    margin-right: calc($boat-sm-width);
  }

  .boat-overlay-container {
    width: calc(100% - $boat-sm-width);

    .boat {
      width: $boat-sm-width;

      img {
        width: $boat-sm-width;
        max-height: $boat-sm-height;
        height: $boat-sm-height;
      }
    }
  }
}


@media all and (max-width: 750px) { //smaller than 750px
  .boat-container {
    min-width: calc(4 * $boat-xsm-width);
    height: $boat-xsm-height;
  }

  .boat-start, .boat-finish {
    img {
      width: $flag-xsm-size;
      height: $flag-xsm-size;
    }
  }
  .boat-start {
    margin-left: calc($boat-xsm-width);
  }

  .boat-finish {
    margin-right: calc($boat-xsm-width);
  }

  .boat-overlay-container {
    width: calc(100% - $boat-xsm-width);

    .boat {
      width: $boat-xsm-width;

      img {
        width: $boat-xsm-width;
        max-height: $boat-xsm-height;
        height: $boat-xsm-height;
      }
    }
  }
}
</style>