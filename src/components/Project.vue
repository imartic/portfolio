<template>

  <div class="logo-container non-selectable">       
    <div class="logo" :style="position">
      
      <div class="home-title">Project</div>
      <div class="home-subtitle">
        
      </div>

    </div>
  </div>

</template>

<script>
var moveForce = 1
var rotateForce = 1.5

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
  width: 70%;
  height: 50%;
  perspective: 800px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translateX(-50%) translateY(-50%);
}
.logo{
  transform-style: preserve-3d;
}

.home-title{
  text-align: center;
  border: 1px solid #bbb;
  font-size: 36px;
  text-shadow: 0px 5px 10px #050505;
  -webkit-text-shadow: 0px 5px 10px #050505;
  -moz-text-shadow: 0px 5px 10px #050505;
  padding: 7px
}
.home-subtitle{
  color: #ddd;
  margin-top: 25px;
  margin-bottom:25px;
  font-size: 17px;
  font-weight: 300;
  text-shadow: 0px 5px 10px #050505;
  -webkit-text-shadow: 0px 5px 10px #050505;
  -moz-text-shadow: 0px 5px 10px #050505;
}

/* porfolio */
.project-card{
  border: 1px solid #bbb;
}
.project-card button i{
  font-size:28px
}
.tech-section{
  margin-top: -17px;
  margin-bottom:15px;
}
.tech-item{
  border:1px solid #bbb;
  color:#999;
  font-size:16px;
  padding:3px 6px 3px 6px;
  margin:3px 7px 3px 0;
  display: inline-block;
}

.card-actions > *:not(:last-child){
  padding: 0
}
</style>
