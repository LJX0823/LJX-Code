<template>
 <div class="slide" v-on:mouseover="stop()" v-on:mouseout="move()">
    <div class="slideshow">
      <transition-group tag="ul" name="image">
        <li v-for="(img, index) in imgArray" v-show="index===mark" :key="index">
          <a href="#">
            <img :src='img'>
          </a>
        </li>
      </transition-group>
    </div>
    <div class="bullet">
      <span v-for="(item, index) in imgArray" :class="{ 'active':index===mark }"
      @click="change(index)" :key="index"></span>
    </div>
  </div>

</template>
<script>

export default {
  data () {
    return {
      timer: null, //定时器
      mark: 0, //比对图片索引的变量
      imgArray: [
        '../../static/img/lb1.png',
        '../../static/img/lb2.png',
        '../../static/img/lb3.png',
      ]
    }
  },
  methods: {
    autoPlay () {
      this.mark++;
      if (this.mark === 3) {
        this.mark = 0
      }
    },
    play () {
      this.timer = setInterval(this.autoPlay, 2500)
    },
    change (i) {
      this.mark = i
    },
    stop () {
      clearInterval(this.timer)
    },
    move () {
      this.timer = setInterval(this.autoPlay, 2500)
    }
  },
  created () {
    this.play()
  }
}
</script>

<style scoped>
  * {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  .slide {
    width: 260px;
    height: 350px;
    margin: -15px auto;
    overflow: hidden;
    position: relative;
  }
  .slideshow {
    width: 260px;
    height: 350px;
  }
  li {
    position: absolute;
  }
  img {
    width: 260px;
    height: 350px;
  }
  .bar {
    position: absolute;
    width: 100%;
    bottom: 10px;
    margin: 0 auto;
    z-index: 10;
    text-align: center;
  }
  .bar span {
    width: 20px;
    height: 5px;
    border: 1px solid;
    background: white;
    display: inline-block;
    margin-right: 10px;
  }
  .active {
    background: red !important;
  }
  .image-enter-active {
    transform: translateX(0);
    transition: all 1.5s ease;
  }
  .image-leave-active {
    transform: translateX(-100%);
    transition: all 1.5s ease;
  }
  .image-enter {
    transform: translateX(100%);
  }
  .image-leave {
    transform: translateX(0);
  }

</style>