<template>
  <div class="computer">
    <div class="navigation">
      <img src="../assets/images/computer.png" alt="" />&nbsp;&gt;&nbsp;我的电脑
    </div>
    <div class="content">
      <ul class="left-box">
        <li class="iconfont">&#xe636;&nbsp;&nbsp;主目录</li>
        <li class="iconfont">&#xe600;&nbsp;&nbsp;视频</li>
        <li class="iconfont">&#xe680;&nbsp;&nbsp;音乐</li>
        <li class="iconfont">&#xe665;&nbsp;&nbsp;图片</li>
        <li class="iconfont">&#xe61f;&nbsp;&nbsp;文档</li>
        <li class="iconfont">&#xe6ad;&nbsp;&nbsp;下载</li>
        <li class="iconfont">&#xe61c;&nbsp;&nbsp;回收站</li>
        <li class="iconfont" style="border-top: 1px solid #b4b4b4">
          &#xe622;&nbsp;&nbsp;计算机
        </li>
        <li class="iconfont">&#xe743;&nbsp;&nbsp;云盘</li>
        <li class="iconfont" style="border-top: 1px solid #b4b4b4">
          &#xe638;&nbsp;&nbsp;网络邻居
        </li>
      </ul>

      <ul class="right-box">
        <li>
          <img src="../assets/images/disk.png" alt="" />
          <div>
            <span class="title">办公</span><span class="progress-bar"></span
            ><span class="xtitle">324G可用</span>
          </div>
        </li>
        <li>
          <img src="../assets/images/disk.png" alt="" />
          <div>
            <span class="title">娱乐</span><span class="progress-bar"></span
            ><span class="xtitle">128G可用</span>
          </div>
        </li>
        <li>
          <img src="../assets/images/disk.png" alt="" />
          <div>
            <span class="title">软件</span><span class="progress-bar"></span
            ><span class="xtitle">78G可用</span>
          </div>
        </li>
        <li>
          <img src="../assets/images/disk.png" alt="" />
          <div>
            <span class="title">文档</span><span class="progress-bar"></span
            ><span class="xtitle">224G可用</span>
          </div>
        </li>
        <li>
          <img src="../assets/images/disk.png" alt="" />
          <div>
            <span class="title">储存</span><span class="progress-bar"></span
            ><span class="xtitle">167G可用</span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>


export default {
  name: "Computer",
  props: {},
  methods: {},
};
</script>

<style scoped>
.computer {
  width: 100%;
  min-height: 100%;
  background: #fff;
}

.navigation {
  display: flex;
  height: 20px;
  line-height: 20px;
  width: 98%;
  margin: 10px auto;
  font-size: 13px;
  color: #333;
  border-radius: 3px;
  border: 1px #a9a9a9 solid;
  cursor: pointer;
}

.navigation img {
  height: 20px;
  margin-left: 5px;
}

.content {
  display: flex;
  height: calc(100% - 30px);
  border-top: 1px solid #b4b4b4;
  box-sizing: border-box;
}

.left-box {
  width: 188px;
  border-right: 1px solid #b4b4b4;
  text-align: left;
  box-sizing: border-box;
}

.left-box li {
  height: 30px;
  line-height: 30px;
  padding-left: 20px;
  font-size: 17px;
  text-align: left;
  color: #333;
  cursor: pointer;
}

.left-box li:hover {
  color: #2da7f8;
  background-color: #d1e8fa;
  border-right: 3px solid #2da7f8;
}

.right-box {
  display: flex;
  flex: 1;
  padding-top: 20px;
  flex-wrap: wrap;
  align-content: flex-start;
}

.right-box li {
  display: flex;
  height: 75px;
  padding: 10px 20px;
  margin-left: 25px;
  margin-top: 10px;
  text-align: center;
  box-sizing: border-box;
  border-radius: 5px;
  cursor: pointer;
}

.right-box li:hover {
  background: #dedede;
}

.right-box li img {
  display: inline-block;
  margin-top: 8px;
  margin-right: 10px;
  width: 45px;
  height: 45px;
}

.right-box li span {
  display: block;
  line-height: 20px;
  font-size: 14px;
  text-align: left;
}

.right-box li .title {
  color: #3e3e3e;
  font-weight: bold;
}

.right-box li .xtitle {
  color: #717171;
}

.progress-bar {
  position: relative;
  background-color: #dedede;
  width: 140px;
  height: 16px;
  border-radius: 3px;
  border: 1px #a9a9a9 solid;
}

.progress-bar:before {
  content: url(../assets/images/bar.png);
  position: absolute;
  top: 0;
  left: 0;
  height: 100%;
  width: 50px;
  overflow: hidden;
  box-sizing: border-box;
}
</style>
