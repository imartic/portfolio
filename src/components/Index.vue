<template>

  <div class="logo-container non-selectable">       
    <div class="logo" :style="position">
      <img class="home-img" src="~assets/me.jpg" height="250px">
      <div class="text-center">
        <div class="home-title">IVAN MARTIĆ</div>
        <div class="home-subtitle">SOFTWARE & WEB DEVELOPER</div>
        
        <br/><br/>
        <router-link to="/about" class="more">
          <button class="grey clear" style="font-weight:400">
            More about me
            <i class="on-right">chevron_right</i>
          </button>
        </router-link>

      </div>
    </div>
  </div>

</template>

<script>
var moveForce = 8
var rotateForce = 14

import { Utils } from 'quasar'

export default {
  data () {
    return {
      moveX: 0,
      moveY: 0,
      rotateY: 0,
      rotateX: 0
    }
  },
  computed: {
    position () {
      let transform = `rotateX(${this.rotateX}deg) rotateY(${this.rotateY}deg)`
      return {
        top: this.moveY + 'px',
        left: this.moveX + 'px',
        '-webkit-transform': transform,
        '-ms-transform': transform,
        transform
      }
    }
  },
  methods: {
    move (event) {
      const {width, height} = Utils.dom.viewport()
      const {top, left} = Utils.event.position(event)
      const halfH = height / 2
      const halfW = width / 2

      this.moveX = (left - halfW) / halfW * -moveForce
      this.moveY = (top - halfH) / halfH * -moveForce
      this.rotateY = (left / width * rotateForce * 2) - rotateForce
      this.rotateX = -((top / height * rotateForce * 2) - rotateForce)
    }
  },
  mounted () {
    this.$nextTick(() => {
      document.addEventListener('mousemove', this.move)
      document.addEventListener('touchmove', this.move)
    })
  },
  beforeDestroy () {
    document.removeEventListener('mousemove', this.move)
    document.removeEventListener('touchmove', this.move)
  }
}
</script>

<style scoped>
.logo-container{
  width: 250px;
  height: 250px;
  perspective: 800px;
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
}
  
.logo{
  position: absolute;
  transform-style: preserve-3d;
}

.home-title{
  border: 1px solid #bbb;
  margin-top: 30px;
  font-size: 36px;
  text-shadow: 0px 5px 10px #050505;
  -webkit-text-shadow: 0px 5px 10px #050505;
  -moz-text-shadow: 0px 5px 10px #050505;
  padding: 7px
}
.home-subtitle{
  margin-top: 10px;
  font-size: 16px;
  font-weight: 300;
  text-shadow: 0px 5px 10px #050505;
  -webkit-text-shadow: 0px 5px 10px #050505;
  -moz-text-shadow: 0px 5px 10px #050505;
}
.home-img{
  border-radius: 50%;
  box-shadow: 0px 5px 10px #050505;
  -webkit-box-shadow: 0px 5px 10px #050505;
  -moz-box-shadow: 0px 5px 10px #050505;
  -webkit-filter: grayscale(100%); 
  filter: grayscale(100%);
}

.more{
  font-weight: 300;
}
</style>
