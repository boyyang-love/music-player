<template>
  <div class="menu">
    <div class="name">
      <a href="https://music.163.com/">
        <i class="iconfont icon-yinle2"></i> BOYYANG
      </a>
    </div>

    <div class="search">
      <input type="text" v-model="name" @keyup.enter="searchmusic" />
      <i class="iconfont icon-sousuo1" @click="searchmusic"></i>
    </div>
  </div>
</template>

<script>
export default {
  name: "Menu",
  componnets: {},
  data() {
    return {
      name: "胡歌",
      songsname: ""
    };
  },
  methods: {
    searchmusic: function() {
      let that = this;
      this.$axios
        .get("https://autumnfish.cn/search?keywords=" + this.name)
        .then(function(res) {
          that.songsname = res.data.result.songs;
          // console.log(res.data.result.songs);
          that.$emit("songs", that.songsname);
        })
        .catch(function(error) {
          console.log(error);
        });
    }
  }
};
</script>

<style scoped>
.menu {
  width: 100%;
  height: 70px;
  background-color: rgb(6, 185, 191);
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.name {
  width: 20%;
}
.search {
  margin-right: 35px;
  width: 20%;
  height: 30px;
  /* border: 1px solid blue; */
  background-color: #8bd1d4;
  border-radius: 30px;
  display: flex;
  justify-content: center;
  align-items: center;
}
a {
  margin-left: 10%;
  text-decoration: none;
  color: white;
  font-size: 24px;
  line-height: 24px;
  font-weight: bold;
}
.search i.iconfont {
  color: white;
  font-weight: bold;
  font-size: 20px;
}
.search i.iconfont:hover {
  color: aqua;
}
input {
  width: 65%;
  border: none;
  outline: none;
  background-color: #8bd1d4;
}
.iconfont {
  width: 20px;
  font-size: 40px;
  color: red;
}
</style>