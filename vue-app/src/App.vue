<template>
  <div id="app">
    <Menu @songs="savesongs" />
    <Mshow :songsname="songsname" @musicurl="musicurl" />
    <Player :musicurl="url" />
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
      url: ""
    };
  },
  methods: {
    savesongs: function(songs) {
      this.songsname = songs;
      // console.log(songs);
    },
    musicurl: function(url) {
      this.url = url;
      console.log(url);
    }
  }
};
</script>

<style>
</style>

