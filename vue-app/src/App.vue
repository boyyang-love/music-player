<template>
  <div id="app">
    <Menu @songs="savesongs" />
    <Mshow :songsname="songsname" @musicurl="musicurl" :iscircle="iscircle" />
    <Player :musicurl="url" @play="play" @pause="pause" />
  </div>
</template>

<script>
import Menu from "./views/Menu";
import Mshow from "./views/Mshow";
import Player from "./views/Player";
export default {
  components: {
    Menu,
    Mshow,
    Player
  },
  data() {
    return {
      songsname: "",
      url: "",
      iscircle: ""
    };
  },
  methods: {
    savesongs: function(songs) {
      this.songsname = songs;
      // console.log(songs);
    },
    musicurl: function(url) {
      this.url = url;
      // console.log(url);
    },
    play: function(play) {
      this.iscircle = play;
    },
    pause: function(pause) {
      this.iscircle = pause;
    }
  }
};
</script>

<style>
</style>

