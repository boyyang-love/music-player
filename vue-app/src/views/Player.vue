<template>
  <div class="player">
    <audio :src="musicurl" autoplay controls></audio>
  </div>
</template>

<script>
export default {
  name: "Player",
  props: ["musicurl"]
};
</script>

<style scoped>
.player {
  width: 100%;
  background-color: aqua;
}
audio {
  height: 50px;
  width: 100%;
}
</style>