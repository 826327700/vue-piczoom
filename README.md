# vue-piczoom

> A picture magnifier component for Vue.js 2.x
基于vue2.x的电商图片放大镜插件

### Build Setup 使用步骤

``` bash
# 安装 install
npm install vue-piczoom --save
```
``` bash
# 使用 use
--script
import PicZoom from 'vue-piczoom'
export default {
  name: 'App',
  components: {
    PicZoom
  }
}

--html
<pic-zoom url="static/imac2.jpg" :scale="3"></pic-zoom>
```
### Config 配置
props | describe | default
----|------|----
url | 图片地址  | string required
big-url | 大图地址 | string null
scale | 图片放大倍数  | number 2.5 
scroll | 放大时页面是否可滚动  | boolean fasle 
show-edit | 是否显示旋转图片按钮  | boolean fasle 

### Suggest 注意事项
组件默认是100%的高宽，所以建议将组件包含在一个有固定高宽的容器内。如：
```
<div class="pic-box"> <!--pic-box:width:500px;height:500px-->
     <pic-zoom url="static/imac2.jpg" :scale="3"></pic-zoom>
</div>
```
### GIF 动画截图
![zoom2.gif](http://upload-images.jianshu.io/upload_images/6651371-e26a702c2ef8651a.gif?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### Demo 示例
[在线示例](https://826327700.github.io/vue-piczoom/dist/ "图片放大镜")