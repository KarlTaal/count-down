<template>
  <button @click="togglePlayMute()">
    <img v-show="isBackgroundSoundPlaying" src="../assets/images/play-sound.png" alt="Play sound">
    <img v-show="!isBackgroundSoundPlaying" src="../assets/images/mute.png" alt="Mute sound">
  </button>
</template>

<script>

import oceanSeaWavesSoundSrc from "@/assets/sounds/ocean-sea-soft-waves.mp3";

export default {
  name: "background-sound",
  data() {
    return {
      oceanSeaWavesSound: new Audio(oceanSeaWavesSoundSrc),
      isBackgroundSoundPlaying: false,
    }
  },
  created() {
    this.startSound();
  },
  methods: {
    startSound() {
      this.oceanSeaWavesSound.loop = true;
      this.oceanSeaWavesSound.play().then(() => this.isBackgroundSoundPlaying = true).catch(() => this.isBackgroundSoundPlaying = false);
    },
    togglePlayMute() {
      this.isBackgroundSoundPlaying = !this.isBackgroundSoundPlaying;
    }
  },
  watch: {
    isBackgroundSoundPlaying(play) {
      if (play) {
        this.startSound()
      } else {
        this.oceanSeaWavesSound.pause();
      }
    }
  }
}


</script>

<style lang="scss" scoped>
button {
  display: flex;
  background: transparent;
  border: unset;
  position: absolute;
  top: 1rem;
  right: 1rem;
  z-index: 100;

  &:hover {
    cursor: pointer;
  }
}

img {
  width: 2rem;
  height: 2rem;
}
</style>