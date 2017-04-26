<template>

  <div class="logo-container non-selectable">       
    <div class="logo" :style="position">
      
      <div class="home-title">About me</div>
      <div class="home-subtitle">
        <p>{{about}}</p>
        <div v-html="getInTouch"></div>
        <div class="tech-section">
            <div>Some technologies I use:</div>
            <div v-for="tech in techIUse" class="tech-item">{{tech}}</div>                            
        </div>
        <div class="lang-section">
            <div>Languages I speak:</div>
            <div v-for="lang in langsISpeak" class="tech-item">{{lang}}</div>                            
        </div>
      </div>

    </div>
  </div>

</template>

<script>
var moveForce = 2
var rotateForce = 4

import { Utils } from 'quasar'

export default {
  data () {
    return {
      moveX: 0,
      moveY: 0,
      rotateY: 0,
      rotateX: 0,
      about: 'I\'m a Software and Web Developer and fresh graduate ' +
             'of Telematics with passion for coding and design. I have over 1 year ' +
             'professional experience as a Software Developer developing mainly for desktop, ' +
             'but have also worked on several web-based projects. Lately I\'m focusing on ' +
             'Front-end web development and learning about the latest frameworks like Vue and ' +
             'React. When I\'m not coding, I try to do some design work and sports.',
      getInTouch: `If you want to get in touch with me, feel free to 
             <a href="mailto:ivan.martic.ri@gmail.com?Subject=Hello!">send me a mail</a>.`,
      techIUse: ['C#', 'MS SQL Server', 'HTML', 'CSS', 'JavaScript', 'jQuery', 'Vue.js'],
      langsISpeak: ['English', 'German', 'Croatian']
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
  position: absolute;
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
  margin-top: 15px;
  margin-bottom:25px;
  font-size: 17px;
  font-weight: 300;
  text-shadow: 0px 5px 10px #050505;
  -webkit-text-shadow: 0px 5px 10px #050505;
  -moz-text-shadow: 0px 5px 10px #050505;
}

.tech-section{margin-top:50px;}
.lang-section{margin-top:20px;}
.tech-item{
  border:1px solid #bbb;
  border-radius:0px;
  color:#bbb;
  font-size:17px;
  padding:4px 8px 4px 8px;
  margin:7px 7px 0 0;
  display: inline-block;
}
</style>
