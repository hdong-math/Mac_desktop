<template>
  <div class="home" :style="{ backgroundImage: 'url(' + bgSrc + ')' }">
    <div class="header">
      <ul class="header-left">
        <li class="iconfont">
          <a href="https://www.apple.com/cn/" target="_blank" title="苹果官网"
            >&#xe60b;</a
          >
        </li>
        <li>
          <a
            href="https://github.com/hdong-math?tab=repositories"
            target="_blank"
            >GitHub</a
          >
        </li>
        <li @click="computer">文件</li>
        <li @click="wallpaper">壁纸</li>
        <li id="about" @click="about">关于</li>
      </ul>
      <ul class="header-right">
        <li class="iconfont">&#xe6c0;</li>
        <li class="iconfont">&#xe688;</li>
        <li class="iconfont" @click="openMusic">&#xe6ca;</li>
        <li class="iconfont">&#xe6a7;</li>
        <li class="iconfont">&#xe6cb;</li>
        <li class="iconfont">&#xe6b8;</li>
        <li class="iconfont" @click="weather">{{ time }}</li>
      </ul>
    </div>
    <div class="content-hone" @click="weatherHide">
      <ul class="app-list">
        <li class="list-item" @click="computer">
          <img src="../assets/images/computer.png" alt="" /><span
            >我的电脑</span
          >
        </li>
        <li class="list-item">
          <img src="../assets/images/TrashIcon.png" alt="" /><span>回收站</span>
        </li>
      </ul>
    </div>
    <div id="container" @click="weatherHide">
      <div id="dock">
        <ul>
          <li>
            <span>Finder</span>
            <img class="pointer" src="../assets/images/1.png" />
          </li>
          <li @click="openBrowser">
            <span>Chrome</span>
            <img class="pointer" src="../assets/images/2.png" />
          </li>
          <li @click="openAppstore">
            <span>App Store</span>
            <img class="pointer" src="../assets/images/4.png" />
          </li>
          <li @click="openMap">
            <span>Map</span>
            <img class="pointer" src="../assets/images/5.png" />
          </li>
          <li>
            <span>Launchpad</span>
            <img class="pointer" src="../assets/images/6.png" />
          </li>
          <li>
            <span>Setup</span>
            <img class="pointer" src="../assets/images/7.png" />
          </li>
          <li>
            <span>Siri</span>
            <img class="pointer" src="../assets/images/8.png" />
          </li>
          <li @click="openMusic">
            <span>iTunes</span>
            <img class="pointer" src="../assets/images/9.png" />
          </li>
        </ul>
      </div>
    </div>

    <transition name="slide-fade">
      <div class="weather" v-show="weatherShow">
        <iframe
          src="https://widget-page.heweather.net/h5/index.html?bg=3&md=036&lc=accu&key=09ce9044126b48f5b79c6d8f198e832a"
        ></iframe>
      </div>
    </transition>
  </div>
</template>

<script>
// @ is an alias to /src
import Music from "@/components/Music.vue";
import Browser from "@/components/Browser.vue";
import Wallpaper from "@/components/Wallpaper.vue";
import Computer from "@/components/Computer.vue";
import About from "@/components/About.vue";
import Map from "@/components/Map.vue";
import Appstore from "@/components/Appstore.vue";
import moment from "moment";
import defaultBg from "../assets/images/bg.jpg"
moment.locale("zh-cn");

export default {
  name: "Home",
  components: {
    Music,
    Wallpaper,
    Browser,
    Computer,
    About,
    Map,
    Appstore,
  },
  data() {
    return {
      time: "",
      setId: null,
      weatherShow: false,
      bgSrc: "",
    };
  },

  created() {
    clearInterval(this.setId);
    this.setId = setInterval(() => {
      /* 实时更新时间 */
      this.newDate();
    }, 1000);
    this.setBg();
    /* 获取缓存壁纸 */
  },

  methods: {
    /* 打开音乐 */
    openMusic() {
      this.$layer.iframe({
        title: "iTunes",
        maxmin: true,
        area: ["70%", "63%"],
        content: {
          content: Music, //传递的组件对象
          parent: this, //当前的vue对象
          data: {}, //props
        },
      });
    },
    /* 打开浏览器 */
    openBrowser() {
      this.$layer.iframe({
        title: "Browser",
        maxmin: true,
        area: ["70%", "60%"],
        content: {
          content: Browser, //传递的组件对象
          parent: this, //当前的vue对象
          data: {}, //props
        },
      });
    },
    /* 打开地图 */
    openMap() {
      this.$layer.iframe({
        title: "Map",
        maxmin: true,
        area: ["70%", "60%"],
        content: {
          content: Map, //传递的组件对象
          parent: this, //当前的vue对象
          data: {}, //props
        },
      });
    },
    /* 打开Appstore */
    openAppstore() {
      this.$layer.iframe({
        title: "App Store",
        maxmin: true,
        area: ["70%", "60%"],
        content: {
          content: Appstore, //传递的组件对象
          parent: this, //当前的vue对象
          data: {}, //props
        },
      });
    },
    /* 打开壁纸 */
    wallpaper() {
      this.$layer.iframe({
        title: "Wallpaper",
        maxmin: true,
        area: ["70%", "60%"],
        content: {
          content: Wallpaper, //传递的组件对象
          parent: this, //当前的vue对象
          data: {}, //props
        },
      });
    },
    /* 打开关于 */
    about() {
      this.$layer.iframe({
        title: "About",
        maxmin: true,
        area: ["70%", "60%"],
        content: {
          content: About, //传递的组件对象
          parent: this, //当前的vue对象
          data: {}, //props
        },
      });
    },
    /* 打开我的电脑 */
    computer() {
      this.$layer.iframe({
        title: "",
        maxmin: true,
        area: ["70%", "60%"],
        content: {
          content: Computer, //传递的组件对象
          parent: this, //当前的vue对象
          data: {}, //props
        },
      });
    },

    weather() {
      this.weatherShow = !this.weatherShow;
    },

    weatherHide() {
      this.weatherShow = false;
    },

    newDate() {
      this.time = moment().format("dddd HH:mm:ss");
    },

    /* 设置壁纸 */
    setBg() {
      if (localStorage.getItem("bg") != null) {
        //获取储存壁纸url
        this.bgSrc = localStorage.getItem("bg");
      } else {
        //设置默认壁纸
        this.bgSrc = defaultBg;
      }
    },
  },
};
</script>

<style>
@import url("../assets/css/common.css");

.home {
  background:  no-repeat no-repeat center;
  background-size: 100% 100%;
}

.header {
  position: relative;
  display: flex;
  height: 30px;
  line-height: 30px;
  background: rgba(15, 15, 0, 0.4);
  color: #fff;
  z-index: 5;
}

.header-left,
.header-right {
  flex: 1;
}

.header-left {
  text-align: left;
}

.header-right {
  text-align: right;
}

.header .header-left li {
  display: inline-block;
  margin: 0 10px;
  cursor: pointer;
}

.header li:hover {
  color: rgb(170, 169, 169);
}

.header a:hover {
  color: rgb(170, 169, 169);
}

.header .header-left li:first-child {
  margin-left: 20px;
}

.header .header-right li {
  display: inline-block;
  margin: 0 5px;
  cursor: pointer;
}

.header .header-right li:last-child {
  margin-right: 10px;
}

.content-hone {
  height: calc(100vh - 30px);
}

.app-list {
  display: flex;
  height: 80vh;
  flex-direction: column;
  flex-wrap: wrap;
  align-content: flex-start;
  padding-left: 20px;
}

.app-list .list-item {
  width: 60px;
  margin-top: 20px;
  margin-left: 25px;
  cursor: pointer;
}

.app-list .list-item img {
  width: 100%;
}

.app-list .list-item span {
  display: block;
  line-height: 21px;
  text-align: center;
  background: rgba(0, 0, 0, 0.2);
  border-radius: 18px;
  margin-top: 8px;
  font-size: 12px;
  color: #ffffff;
}

#container {
  position: fixed;
  bottom: 0;
  left: calc(50% - 400px);
  width: 800px;
  padding: 16px 0;
  background: rgba(15, 15, 0, 0.45);
  border-radius: 10px 10px 0 0;
  text-align: center;
}

#container #dock {
  width: 100%;
  text-align: center;
  margin: 0 auto;
}

#container li {
  list-style-type: none;
  display: inline-block;
  position: relative;
  margin-left: 10px;
}

#container li img {
  width: 50px;
  height: 50px;
  -webkit-box-reflect: below 2px -webkit-gradient(linear, left top, left bottom, from(transparent), color-stop(0.7, transparent), to(rgba(255, 255, 255, 0.5)));
  transition: all 0.3s;
  transform-origin: 40% 70%;
}

#container li:hover img {
  transform: scale(2);
  margin: 0 2em;
}

#container li:hover + li img {
  transform: scale(1.5);
  margin: 0 1.5em;
}

#container li span {
  display: none;
  white-space: nowrap;
  position: absolute;
  bottom: 100px;
  left: 0;
  width: calc(100% - 10px);
  margin-left: 10px;
  background-color: rgba(15, 15, 0, 0.5);
  padding: 4px 0;
  border-radius: 7px;
}

#container li:hover span {
  display: block;
  color: #fff;
}

.weather {
  position: fixed;
  top: 30px;
  right: 0;
}

.weather iframe {
  height: calc(100vh - 30px);
  border: none;
}

.vl-notify-content {
  height: 100% !important;
}

.vl-notice-title {
  background-color: rgb(221, 220, 220) !important;
  border-radius: 5px 5px 2px 2px;
}

.vl-notify.vl-notify-main {
  border-radius: 5px 5px 2px 2px !important;
  border: none !important;
}

.icon-remove:before {
  content: "●" !important;
  font-size: 40px;
  color: red;
  position: absolute;
  left: -1325px;
  top: -4px;
}

.icon-remove:hover:after {
  content: "\2716";
  font-size: 5px;
  color: rgb(221, 220, 220);
  position: absolute;
  left: -1317px;
  top: -1px;
}

.vlicon-max:before {
  content: "●" !important;
  font-size: 40px;
  color: rgb(43, 199, 43);
  position: absolute;
  left: 58px;
  top: -3.5px;
}

.vlicon-max:hover:after {
  content: "+";
  font-size: 22px;
  color: rgb(221, 220, 220);
  position: absolute;
  left: 63px;
  top: -3.5px;
}

.vlicon-mini:before {
  content: "●" !important;
  font-size: 40px;
  color: rgb(247, 173, 34);
  position: absolute;
  left: 32px;
  top: -3.5px;
}

.vlicon-mini:hover:after {
  content: "-";
  font-size: 30px;
  color: rgb(221, 220, 220);
  position: absolute;
  left: 38px;
  top: -4px;
}

.vlicon-huanyuan:before {
  content: "●" !important;
  font-size: 40px;
  color: rgb(43, 199, 43);
}

.lv-title {
  text-align: center;
}

#about {
  background-image: -webkit-linear-gradient(
    left,
    #00ffd5,
    #008cff 16.6%,
    #00ffd5 33.2%,
    #008cff 49.8%,
    #00ffd5 66.4%,
    #008cff 82%,
    #00ffd5 100%
  );
  background-clip: text;
  -webkit-text-fill-color: transparent;
  background-size: 200% 100%;
}

#about:hover{
  background-position: -100%;
  transition:all 1s linear;
}

</style>
