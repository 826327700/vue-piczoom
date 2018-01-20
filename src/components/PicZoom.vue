<template>
    <div class="magnifier-box" :ref="id" @mousemove="mousemove" @mouseover="mouseover" @mouseleave="mouseleave">
        <img :src="url" alt="">
        <div class="mouse-cover"></div>
    </div>
</template>

<script>
    export default {
        props:{
            scale:{
                type:Number,
                default:2.5
            },
            url:{
                type:String,
                required:true
            },
            bigUrl:{
                type:String,
                default:null
            },
            scroll:{
                type:Boolean,
                default:false
            }
        },
        data () {
            return {
                id:null,
                cover:null,
                imgbox:null,
                imgwrap:null,
                img:null,
                canvas:null,
                ctx:null,
                rectTimesX:0,
                rectTimesY:0,
                imgTimesX:0,
                imgTimesY:0,
                init:false
            }
        },
        created(){
        　　var $chars = 'ABCDEFGHJKMNPQRSTWXYZabcdefhijkmnprstwxyz2345678';    /****默认去掉了容易混淆的字符oOLl,9gq,Vv,Uu,I1****/
        　　var maxPos = $chars.length;
        　　var str = '';
        　　for (let i = 0; i < 10; i++) {
                str += $chars.charAt(Math.floor(Math.random() * maxPos));
        　　}
            this.id=str
        },
        mounted(){
            this.$nextTick(()=>{
                this.initBox()
            })
        },
        methods: {
            initBox(){
                let box=this.$refs[this.id]
                this.imgbox=box
                this.cover=box.querySelector('.mouse-cover')
                this.cover.style.width=(this.imgbox.offsetWidth/this.scale)+'px'
                this.cover.style.height=(this.imgbox.offsetHeight/this.scale)+'px'
                this.cover.style.left='-100%'
                this.cover.style.top='-100%'
                this.imgwrap=box.querySelector('img')
                let imgsrc;
                if(this.bigUrl){
                    imgsrc=this.bigUrl
                }else{
                    imgsrc=this.imgwrap.src
                }
                this.img=new Image()
                this.img.src=imgsrc
                this.img.onload=()=>{
                    this.rectTimesX=this.cover.offsetWidth/this.imgwrap.offsetWidth,
                    this.rectTimesY=this.cover.offsetHeight/this.imgwrap.offsetHeight

                    this.imgTimesX=this.img.width/this.imgwrap.offsetWidth,
                    this.imgTimesY=this.img.height/this.imgwrap.offsetHeight
                }

                if(!this.canvas){
                    this.canvas=document.createElement('canvas')
                    this.canvas.className='mouse-cover-canvas'
                    this.canvas.style.position='absolute'
                    this.canvas.style.left=this.imgbox.offsetLeft+this.imgbox.offsetWidth+10+'px'
                    this.canvas.style.top=this.imgbox.offsetTop+'px'
                    this.canvas.style.border='1px solid #eee'
                    this.canvas.style.zIndex='99999'
                    this.canvas.height=this.imgbox.offsetHeight
                    this.canvas.width=this.imgbox.offsetWidth
                    this.canvas.style.display='none'
                    document.body.append(this.canvas)
                }
                this.ctx=this.canvas.getContext("2d");
                this.init=true
            },
            mousemove(e){
                if(!this.init){
                    return false
                }
                let _this=this
                
                function getXY(eve) {
                    return {x : eve.pageX -(_this.cover.offsetWidth/2),y : eve.pageY-(_this.cover.offsetHeight/2) };
                }
                var oEvent = e || event;
                var pos = getXY(oEvent);
                
                if(pos.x<=this.imgwrap.offsetLeft+this.imgwrap.offsetWidth-this.cover.offsetWidth&&pos.x>=this.imgwrap.offsetLeft){
                    this.cover.style.left=pos.x+'px'
                }
                if(pos.y<=this.imgwrap.offsetTop+this.imgwrap.offsetHeight-this.cover.offsetHeight&&pos.y>=this.imgwrap.offsetTop){
                    this.cover.style.top=pos.y+'px'
                }
                if(pos.x<=this.imgwrap.offsetLeft+this.imgwrap.offsetWidth-this.cover.offsetWidth&&pos.x>=this.imgwrap.offsetLeft&&pos.y<=this.imgwrap.offsetTop+this.imgwrap.offsetHeight-this.cover.offsetHeight&&pos.y>=this.imgwrap.offsetTop){

                    this.ctx.clearRect(0,0,this.imgwrap.offsetWidth,this.imgwrap.offsetHeight);
                    let startX=this.cover.offsetLeft-this.imgwrap.offsetLeft,
                    startY=this.cover.offsetTop-this.imgwrap.offsetTop
                    this.ctx.drawImage(this.img,startX*this.imgTimesX,startY*this.imgTimesY,this.img.width*this.rectTimesX,this.img.height*this.rectTimesY,0,0,this.imgbox.offsetWidth,this.imgbox.offsetHeight);
                }
                
            },
            mouseover(e){
                if(!this.init){
                    return false
                }
                e=e||event
                if(!this.scroll){
                    e.currentTarget.addEventListener("mousewheel",function(ev){
                        ev.preventDefault();
                    },false);

                    e.currentTarget.addEventListener("DOMMouseScroll",function(ev){
                        ev.preventDefault();
                    },false);
                }
                
                this.cover.style.display='block'
                this.canvas.style.display='block'
            },
            mouseleave(){
                if(!this.init){
                    return false
                }
                this.cover.style.display='none'
                this.canvas.style.display='none'
            }
        }
    }
</script>

<style lang="scss" scoped>
    .magnifier-box{
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
        overflow: hidden;
        position: static;
        img{
            width: 100%;
        };
        .mouse-cover{
            position: absolute;
            background-color: rgba(0,0,0,0.5);
            cursor:move
        };
        .mouse-cover-canvas{
            position:absolute;
            left:100%;
            top:0;
            width:100%;
            height:100%;
        }
    }
</style>

