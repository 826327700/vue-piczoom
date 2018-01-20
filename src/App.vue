<template>
  <div id="app">
      <div class="pic-box">
        <pic-zoom url="static/imac2.jpg" big-url="static/imac2.jpg" :scale="3"></pic-zoom>
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
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.pic-box{
  width:500px;
  height:500px;
  border:1px solid #eee;
}
</style>
