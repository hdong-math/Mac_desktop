<template>
  <div class="music">
    <div class="play_wrap">
      <div class="search_bar">
        <!-- 搜索歌曲 -->
        <li class="iconfont apple">&#xe60b;</li>
        iTunes Music
        <input
          type="text"
          placeholder="搜索"
          v-model="query"
          @keyup.enter="searchMusic()"
        />
        <li class="iconfont search" @click="searchMusic()">&#xe688;</li>
      </div>
      <div class="center_con">
        <!-- 搜索歌曲列表 -->
        <div class="song_wrapper" ref="song_wrapper">
          <ul class="song_list">
            <li v-for="item in musicList">
              <!-- 点击放歌 -->
              <a href="javascript:;" @click="playMusic(item.id)"></a>
              <b>{{ item.name }}    </b><b id="name">{{item.artists[0].name}}</b>
              <span>
                <i @click="playMv(item.mvid)" v-if="item.mvid != 0"></i>
              </span>
            </li>
          </ul>
          <img
            src="https://i.loli.net/2020/03/23/dor23bhZtIvK17X.png"
            class="switch_btn"
            alt=""
          />
        </div>
        <!-- 歌曲信息容器 -->
        <div class="player_con" :class="{ playing: isPlay }">
          <img
            src="https://i.loli.net/2020/03/23/gZHko2WlpJNcGPv.png"
            class="play_bar"
          />
          <!-- 黑胶碟片 -->
          <img
            src="https://i.loli.net/2020/03/23/hQPuH4gNRx7XayI.png"
            class="disc autoRotate"
          />
          <img
            :src="
              coverUrl == ''
                ? 'https://i.loli.net/2020/03/23/QEL4rdy5KCsn3cz.png'
                : coverUrl
            "
            class="cover autoRotate"
          />
        </div>
        <!-- 评论容器 -->
        <div class="comment_wrapper" ref="comment_wrapper">
          <h5 class="title">热门评论</h5>
          <hr />
          <div class="comment_list">
            <dl v-for="item in hotComments">
              <dt>
                <img :src="item.user.avatarUrl" alt="" />
              </dt>
              <dd class="name">{{ item.user.nickname }}</dd>
              <dd class="detail">
                {{ item.content }}
              </dd>
            </dl>
          </div>
          <img
            src="https://i.loli.net/2020/03/23/dor23bhZtIvK17X.png"
            class="right_line"
          />
        </div>
      </div>
      <div class="audio_con">
        <audio
          ref="audio"
          @play="play"
          @pause="pause"
          :src="musicUrl"
          controls
          autoplay
          loop
          class="myaudio"
        ></audio>
      </div>
      <div class="video_con" v-show="showVideo">
        <video
          ref="video"
          :src="mvUrl"
          controls="controls"
          autoplay="true"
        ></video>
        <div class="mask" @click="closeMv"></div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
axios.defaults.baseURL = "https://autumnfish.cn";

export default {
  name: "Music",
  data() {
    return {
      // 搜索关键字
      query: "",
      // 歌曲列表
      musicList: [],
      // 歌曲url
      musicUrl: "",
      // 是否正在播放
      isPlay: false,
      // 歌曲热门评论
      hotComments: [],
      // 歌曲封面地址
      coverUrl: "",
      // 显示视频播放
      showVideo: false,
      // mv地址
      mvUrl: "",
    };
  },
  // 方法
  methods: {
    // 搜索歌曲
    searchMusic() {
      if (this.query == 0) {
        return;
      }
      axios.get("/search?keywords=" + this.query).then((response) => {
        // 保存内容
        this.musicList = response.data.result.songs;
        console.log(this.musicList)
      });

      // 清空搜索
      this.query = "";
    },
    // 播放歌曲
    playMusic(musicId) {
      // 获取歌曲url
      axios.get("/song/url?id=" + musicId).then((response) => {
        // 保存歌曲url地址
        this.musicUrl = response.data.data[0].url;
      });
      // 获取歌曲热门评论
      axios.get("/comment/hot?type=0&id=" + musicId).then((response) => {
        
        // 保存热门评论
        this.hotComments = response.data.hotComments;
      });
      // 获取歌曲封面
      axios.get("/song/detail?ids=" + musicId).then((response) => {
        
        // 设置封面
        this.coverUrl = response.data.songs[0].al.picUrl;
      });
    },
    // audio的play事件
    play() {
      this.isPlay = true;
      // 清空mv的信息
      this.mvUrl = "";
    },
    // audio的pause事件
    pause() {
      this.isPlay = false;
    },
    // 播放mv
    playMv(vid) {
      if (vid) {
        this.showVideo = true;
        // 获取mv信息
        axios.get("/mv/url?id=" + vid).then((response) => {
          // console.log(response)
          // 暂停歌曲播放
          this.$refs.audio.pause();
          // 获取mv地址
          this.mvUrl = response.data.data.url;
        });
      }
    },
    // 关闭mv界面
    closeMv() {
      this.showVideo = false;
      this.$refs.video.pause();
    },
  },
};
</script>

<style scoped>
.music {
  width: 100%;
  min-height: 100%;
  background: #fff;
}

.play_wrap {
  width: 100%;
  min-height: 100%;
  background-color: #d8d7d7;
}

.search_bar {
  height: 60px;
  background-image: -webkit-linear-gradient(
    top,
    rgb(228, 228, 228),
    rgb(187, 187, 187)
  );
  border-bottom: 2px solid rgb(170, 170, 170);
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
  z-index: 11;
  font-weight: bold;
}

.search_bar input {
  margin-left: auto;
  margin-right: 23px;
  width: 220px;
  height: 34px;
  border-radius: 17px;
  border: 0px;
  background: rgba(255, 255, 255, 0.45);
  text-indent: 15px;
  outline: none;
}

.search {
  position: absolute;
  right: 40px;
  font-size: 20px;
  cursor: pointer;
  color: rgb(150, 149, 149);
}

.search:hover {
  color: rgb(126, 126, 126);
}

.apple {
  font-size: 23px;
  margin-left: 50px;
  margin-right: 30px;
}

.center_con {
  height: 435px;
  background-color: rgba(255, 255, 255, 0.5);
  display: flex;
  position: relative;
}

.song_wrapper {
  width: 300px;
  height: 435px;
  box-sizing: border-box;
  padding: 10px 0;
  list-style: none;
  position: absolute;
  left: 0px;
  top: 0px;
  z-index: 1;
}

.song_list {
  width: 100%;
  overflow-y: auto;
  overflow-x: hidden;
  height: 100%;
}
.song_list::-webkit-scrollbar {
  display: none;
}

.song_list li {
  font-size: 14px;
  height: 40px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  width: 580px;
  padding-left: 10px;
}

.song_list li:nth-child(odd) {
  background-color: rgba(206, 206, 206, 0.2);
}

.song_list li a {
  display: block;
  position: relative;
  width: 0px;
  height: 0px;
  border-top: 7px solid transparent;
  border-bottom: 7px solid transparent;
  border-right: 5px solid transparent;
  border-left: 10px solid black;
  margin-right: 10px;
  margin-left: 10px;
}
.song_list li a:after {
  display: block;
  content: "";
  position: absolute;
  right: -6px;
  top: -12px;
  border: 12px solid rgba(0, 0, 0, 0.2);
  border-radius: 50%;
}

.song_list li b {
  font-weight: normal;
  width: 120px;
  overflow: auto;
  white-space: pre;
}

#name{
  width:55px;
  margin-left:25px;
}

.song_list li b::-webkit-scrollbar {
  display: none;
}

.song_list li span {
  width: 23px;
  height: 17px;
  margin-left: 40px;
}

.song_list li span i {
  display: block;
  position: relative;
  right:20px;
  width: 0px;
  height: 0px;
  border-top: 7px solid transparent;
  border-bottom: 7px solid transparent;
  border-right: 5px solid transparent;
  border-left: 10px solid black;
  cursor: pointer;
}

.song_list li span i::after {
  display: block;
  content: "";
  position: absolute;
  right: -6px;
  top: -12px;
  border: 12px solid rgba(0, 0, 0, 0.2);
  border-radius: 15%;
}

.player_con {
  width: 400px;
  height: 435px;
  position: absolute;
  left: 300px;
  top: 0px;
}

.disc {
  position: absolute;
  left: 65px;
  top: 50px;
  border: 15px solid rgb(192, 192, 192);
  border-radius:50%;
  z-index: 9;
}
.cover {
  position: absolute;
  left: 130px;
  top: 115px;
  width: 150px;
  height: 150px;
  border-radius: 75px;
  z-index: 8;
}
.comment_wrapper {
  width: 600px;
  height: 435px;
  list-style: none;
  position: absolute;
  left: 700px;
  top: 0px;
  padding: 25px 10px;
}
.comment_wrapper .title {
  position: absolute;
  top: 0;
  margin: 10px;
  font-size: 16px;
}
hr {
  width: 600px;
  position: absolute;
  border-bottom: none;
  top: 43px;
  box-shadow: 0px 2.3px 5px #000000;
}

.comment_wrapper .comment_list {
  overflow: auto;
  margin-top: 20px;
  height: 410px;
}
.comment_wrapper .comment_list::-webkit-scrollbar {
  display: none;
}
.comment_wrapper dl {
  padding-top: 10px;
  padding-left: 55px;
  position: relative;
  margin-bottom: 20px;
}

.comment_wrapper dt {
  position: absolute;
  left: 4px;
  top: 14px;
  width: 45px;
  height: 45px;
  border-radius: 15px;
  overflow: hidden;
  border: 2px solid rgb(122, 122, 122);
}

.comment_wrapper dt img {
  width: 45px;
  height: 45px;
}

.comment_wrapper dd {
  font-size: 14px;
  margin-left: 10px;
}

.comment_wrapper .name {
  font-weight: bold;
  color: #333;
  padding-top: 5px;
}

.comment_wrapper .detail {
  color: #666;
  margin-top: 5px;
  line-height: 18px;
}
.audio_con {
  height: 50px;
  background-color: #f1f3f4;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
}
.myaudio {
  width: 1300px;
  height: 40px;
  margin-top: 5px;
  outline: none;
  background-color: #f1f3f4;
}

/* 旋转的动画 */
@keyframes Rotate {
  from {
    transform: rotateZ(0);
  }
  to {
    transform: rotateZ(360deg);
  }
}
/* 旋转的类名 */
.autoRotate {
  animation-name: Rotate;
  animation-iteration-count: infinite;
  animation-play-state: paused;
  animation-timing-function: linear;
  animation-duration: 5s;
}
/* 是否正在播放 */
.player_con.playing .disc,
.player_con.playing .cover {
  animation-play-state: running;
}

.play_bar {
  position: absolute;
  left: 200px;
  top: -10px;
  z-index: 10;
  transform: rotate(-25deg);
  transform-origin: 12px 12px;
  transition: 1s;
}
/* 播放杆 转回去 */
.player_con.playing .play_bar {
  transform: rotate(0);
}

.switch_btn {
  position: absolute;
  right: 0;
  top: 0;
  cursor: pointer;
}
.right_line {
  position: absolute;
  left: 0;
  top: 0;
}
.video_con video {
  position: fixed;
  width: 800px;
  height: 480px;
  left: 50%;
  top: 50%;
  margin-top: -220px;
  transform: translateX(-50%);
  z-index: 990;
}
.video_con .mask {
  position: fixed;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  z-index: 980;
  background-color: rgba(0, 0, 0, 0.8);
}
</style>
