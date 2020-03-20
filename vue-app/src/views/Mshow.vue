<template>
  <div class="mshow">
    <div class="mlist">
      <ul>
        <li v-for="(item,i) in songsname" :key="i" @click="musicplay(item)">
          <i class="iconfont icon-bofang1 start"></i>
          <a href="#">{{item.name}}</a>
          <i class="iconfont icon-MV end"></i>
        </li>
      </ul>
    </div>
    <div class="mvplay"></div>
    <div class="hotcomments"></div>
  </div>
</template>

<script>
export default {
  name: "Mshow",
  data() {
    return {
      musicurl: ""
    };
  },
  props: ["songsname"],
  methods: {
    musicplay: function(item) {
      let that = this;
      this.$axios
        .get("https://autumnfish.cn/song/url?id=" + item.id)
        .then(res => {
          that.musicurl = res.data.data[0].url;
          //   console.log(res.data.data[0].url);
          that.$emit("musicurl", that.musicurl);
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style scoped>
.mshow {
  width: 100%;
  height: 500px;
  background-color: aqua;
  display: flex;
}
.mlist {
  flex: 1;
  border-right: 1px solid goldenrod;
  overflow: scroll;
}
.mvplay {
  flex: 2;
  border-right: 1px solid goldenrod;
}
.hotcomments {
  flex: 1;
}
ul {
  margin: 0;
  padding: 0;
  list-style: none;
  display: flex;
  flex-wrap: wrap;
}
ul li {
  display: flex;
  height: 23px;
  width: 100%;
  margin-top: 5px;
}
.start {
  flex: 1;
  width: 25px;
  height: 25px;
  align-self: flex-start;
}
.end {
  flex: 1;
  align-self: flex-end;
}
ul li:hover {
  background-color: hotpink;
}
a {
  flex: 3;
  text-decoration: none;
  color: white;
  font-size: 20px;
  line-height: 18px;
  margin-left: 5px;
}
i {
  font-size: 20px;
  color: brown;
}
</style>