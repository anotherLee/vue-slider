<template>
  <div class="hello">
    <div class="box-wrapper" @mouseenter="stop" @mouseleave="restart">
      <ul class="directions">
        <li class="left" @click="lastImage">&lt;</li>
        <li class="right" @click="nextImage">&gt;</li>
      </ul>
      <transition-group tag="ul" class="box" name="list">
        <li v-for="(item, index) in images" :key="index" v-show="nowIndex === index">
          <img :src="item.url" alt="item.description">
        </li>
      </transition-group>
      <div class="carousel-item">
        <span v-for="(item, index) in images.length" :key="index" @click="jump(index)" :class="{active: nowIndex === index}">{{index+1}}</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      images:[
        {
          url: "../../static/images/banner01.png",
          description: 'image01'
        },
        {
          url: '../../static/images/banner02.png',
          description: 'image02'
        },
        {
          url: '../../static/images/banner03.png',
          description: 'images03'
        }
      ],
      nowIndex:0
    }
  },
  mounted () {
    this.autoPlay()
  },
  methods:{
    nextImage: function () {
      this.nowIndex++
      this.nowIndex = this.nowIndex > 2 ? 0 : this.nowIndex
    },
    lastImage: function () {
      this.nowIndex--
      this.nowIndex = this.nowIndex < 0 ? 2 : this.nowIndex
    },
    jump: function (index) {
      this.nowIndex = index
    },
    autoPlay: function () {
      let that = this
      this.clock = setInterval(function () {
        that.nowIndex++
        that.nowIndex = that.nowIndex > 2 ? 0 : that.nowIndex
      },3000)
    },
    stop: function () {
      clearInterval(this.clock)
    },
    restart: function () {
      this.autoPlay()
    }
  }
}
</script>

<style>
*{
  padding:0;
  margin:0;
  box-sizing:border-box;
}
ul{
  list-style: none;
}
.box-wrapper{
  position:relative;
}
.directions li{
  position:absolute;
  top:50%;
  transform:translateY(-50%);
  display: flex;
  justify-content: center;
  align-items:center;
  z-index:1;
  font-size:25px;
  color:#fff;
  width:50px;
  height: 120px;
  background-color:rgba(0,0,0,0.1);
  cursor:pointer;
  -webkit-touch-callout: none;
  -webkit-user-select: none;
  -khtml-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}
.directions .left{
  left:10px;
}
.directions .right{
  right:10px;
}
.box-wrapper{
  width:1200px;
  height:500px;
  margin:0 auto;
}
.box{
  position:relative;
  width:100%;
  height:100%;
  overflow:hidden;
}
.box li{
  position: absolute;
  left: 0;
  top:0;
}
.carousel-item span{
  display:inline-block;
  width:25px;
  height: 25px;
  margin:5px;
  line-height:25px;
  border:1px solid #ccc;
  border-radius:50%;
  cursor:pointer;
}
.active{
  background-color:#ccc;
}

.list-enter-active {
  transition: all .8s ease;
  transform: translateX(0);
}

.list-leave-active {
  transition: all 0.8s ease;
  transform: translateX(-100%);
}

.list-enter {
  transform: translateX(100%);
}

.list-leave {
  transform: translateX(0);
}

</style>
