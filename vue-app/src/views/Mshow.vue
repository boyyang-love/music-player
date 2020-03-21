<template>
  <div class="mshow">
    <div class="mlist">
      <ul>
        <li v-for="(item,i) in songsname" :key="i" :class="{checked:i==n}">
          <i class="iconfont icon-bofang1 start" @click="musicplay(item,i)"></i>
          <a href="#" @click="musicplay(item,i)">{{item.name}}</a>
          <i class="iconfont icon-MV end" @click="playmv(item)" v-show="item.mvid !=0"></i>
        </li>
      </ul>
    </div>
    <div class="mvplay">
      <div :class="{circle:iscircle}" v-show="isplay">
        <img :src="img" alt />
      </div>
    </div>
    <div class="hotcomments">
      <ul>
        <li v-for="(item,i) in musichotcomments" :key="i">
          <span class="pho">
            <img :src="item.user.avatarUrl" alt />
          </span>
          <span class="hot">
            <h5>{{item.user.nickname}}</h5>
            <h4>{{item.content}}}</h4>
          </span>
        </li>
      </ul>
    </div>
    <div class="mv" v-show="flog">
      <video id="player" :src="mvurl" controls autoplay></video>
      <div class="mask" @dblclick="closemv"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Mshow",
  data() {
    return {
      musicurl: "",
      musichotcomments: "",
      n: "",
      flog: false,
      isplay: false,
      // iscircle: true,
      mvurl: "",
      img: ""
      // checked: false
    };
  },
  props: ["songsname", "iscircle"],
  methods: {
    musicplay: function(item, i) {
      this.n = i;
      // console.log(i);
      let that = this;
      this.$axios
        .get("https://autumnfish.cn/song/url?id=" + item.id)
        .then(res => {
          that.musicurl = res.data.data[0].url;
          // console.log(res);
          that.$emit("musicurl", that.musicurl);
        })
        .catch(error => {
          console.log(error);
        });

      this.$axios
        .get("https://autumnfish.cn/comment/hot?type=0&id=" + item.id)
        .then(res => {
          that.musichotcomments = res.data.hotComments;
          // console.log(res.data.hotComments);
        })
        .catch(error => {
          console.log(error);
        });
      this.$axios
        .get("https://autumnfish.cn/song/detail?ids=" + item.id)
        .then(res => {
          // console.log(res.data.songs[0].al.picUrl);
          that.isplay = true;
          that.img = res.data.songs[0].al.picUrl;
        })
        .catch(error => {
          console.log(error);
        });
    },
    playmv: function(item) {
      this.flog = true;
      let that = this;
      this.$axios
        .get("https://autumnfish.cn/mv/url?id=" + item.mvid)
        .then(res => {
          that.mvurl = res.data.data.url;
          // console.log(res.data.data.url);
        })
        .catch(error => {
          console.log(error);
        });
    },
    closemv: function() {
      this.flog = false;
      let video = document.getElementById("player");
      video.pause();
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
.checked {
  background-color: coral;
}
.mvplay {
  flex: 2;
  border-right: 1px solid goldenrod;
  display: flex;
  justify-content: center;
  align-items: center;
}
.mvplay div {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}
div.mv {
  display: flex;
  width: 100%;
  height: 100%;
  justify-content: center;
}
.mv video {
  width: 70%;
  z-index: 999;
}
.mask {
  width: 100%;
  height: 80%;
  position: fixed;
  z-index: 99;
}
.hotcomments {
  flex: 1;
  overflow: scroll;
}
.mlist ul {
  margin: 0;
  padding: 0;
  list-style: none;
  display: flex;
  flex-wrap: wrap;
}
.mlist ul li {
  display: flex;
  height: 23px;
  width: 100%;
  margin-top: 5px;
  overflow: hidden;
}
.start {
  flex: 1;
  width: 25px;
  height: 25px;
  align-self: flex-start;
}
.end {
  flex: 1;
  width: 50%;
  align-self: flex-end;
}
i.end:hover {
  color: red;
}
.mlist ul li:hover {
  background-color: hotpink;
}
a {
  flex: 9;
  text-decoration: none;
  color: white;
  font-size: 16px;
  line-height: 18px;
  margin-left: 5px;
}
i {
  font-size: 20px;
  color: brown;
}

.hotcomments ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
.hotcomments ul li {
  display: flex;
  margin-top: 20px;
}
span.pho {
  align-self: start;
}
.pho img {
  width: 120px;
  height: 120px;
  border-radius: 100%;
}
h5 {
  margin: 0;
  color: white;
  font-size: 18px;
  font-weight: bold;
}
.mvplay img {
  width: 200px;
  height: 200px;
  border-radius: 100%;
  border: 80px solid black;
}

.circle img {
  width: 200px;
  height: 200px;
  border-radius: 100%;
  border: 80px solid black;
  animation: zhuan 5s infinite;
  transition-timing-function: linear;
  transition-delay: 0s;
}

@keyframes zhuan {
  from {
    transform: rotateZ(0deg);
  }
  to {
    transform: rotateZ(360deg);
  }
}
</style>