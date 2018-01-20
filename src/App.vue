<template>
  <div id="app">
      <p>配置3倍放大：<span style="color:#ff6600">:scale="3"</span></p>
      <div class="pic-box">
        <pic-zoom url="static/imac2.jpg" :scale="3"></pic-zoom>
      </div>
      <p>配置放大时可滚动页面(滚轮)：<span style="color:#ff6600">:scroll="true"</span></p>
      <div class="pic-box">
        <pic-zoom url="static/imac2.jpg" :scale="3" :scroll="true"></pic-zoom>
      </div>
      <p>分开配置大小图片地址：<span style="color:#ff6600">url="static/imac2_thumb.jpg" big-url="static/imac2.jpg"</span></p>
      <div class="pic-box">
        <pic-zoom url="static/imac2_thumb.jpg" big-url="static/imac2.jpg" :scale="3" ></pic-zoom>
      </div>
  </div>
</template>

<script>
import PicZoom from './components/PicZoom'

export default {
  name: 'App',
  components: {
    PicZoom
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.pic-box{
  width:500px;
  height:500px;
  border:1px solid #eee;
}
</style>
