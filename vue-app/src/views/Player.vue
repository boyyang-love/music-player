<template>
  <div class="player">
    <audio :src="musicurl" autoplay controls @play="play" @pause="pause"></audio>
  </div>
</template>

<script>
export default {
  name: "Player",
  props: ["musicurl"],
  methods: {
    play: function() {
      this.$emit("play", true);
    },
    pause: function() {
      this.$emit("pause", false);
    }
  }
};
</script>

<style scoped>
.player {
  width: 100%;
}
audio {
  height: 50px;
  width: 100%;
}
</style>