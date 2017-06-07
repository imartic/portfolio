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

        <div class="about-footer">
          <button class="cv-btn clear grey outline" @click="$refs.cvModal.toggle()">
            <i class="on-left">open_in_new</i>
            View my CV
          </button>
        </div>

      </div>

      <!-- cv modal -->
      <q-modal ref="cvModal" class="full-modal minimized" 
        :content-css="{width: '460px', height: '470px'}">
        <q-layout>

            <div class="layout-view">
                <button class="close-modal-cv text-shadow" @click="$refs.cvModal.toggle()">
                    <i>close</i>
                </button>
                <div class="layout-padding text-center cv-modal-layout">
                    <h5 class="modal-title-cv text-shadow">Choose language of CV</h5>
                    <hr class="info-divider"/>
                    <div class="list cv-list">
                      <label class="item text-shadow" v-for="item in cv_langs">
                        <div class="item-primary">
                          <q-radio :disable="item.value != 'en'"
                            v-model="cv_lang"  
                            :val="item.value">
                          </q-radio>
                        </div>
                        <div class="item-content">
                          {{ item.text }}
                        </div>
                      </label>
                    </div>

                    <button class="cv-confirm-btn clear grey outline" @click="viewCV()">
                      <i class="on-left">open_in_new</i>
                      Open
                    </button>
                </div>
            </div>

        </q-layout>
    </q-modal>

    </div>
  </div>

</template>

<script>
var moveForce = 0.2
var rotateForce = 1.5

import { Utils } from 'quasar'

// loading cvs with file-loader (isntallation: npm install --save-dev file-loader)
var cvEn = require('file-loader?name=[name].[ext]!../files/IvanMarticCV_en.pdf')

export default {
  data () {
    return {
      moveX: 0,
      moveY: 0,
      rotateY: 0,
      rotateX: 0,
      about: 'I\'m a Software and Web Developer and fresh graduate ' +
             'of Telematics with passion for coding and design. I have over 1 year ' +
             'professional experience as a Software Developer developing desktop and web applications. ' +
             'Lately I\'m focusing on ' +
             'Front-end web development and learning about the latest frameworks like Vue and ' +
             'React. When I\'m not coding, I try to do some design work and sports.',
      getInTouch: `If you want to get in touch with me, feel free to 
             <a href="mailto:ivan.martic.ri@gmail.com?Subject=Hello!">send me a mail</a>.`,
      techIUse: ['C#', 'MS SQL Server', 'HTML', 'CSS', 'JavaScript', 'jQuery', 'Vue.js', 'GIT', 'TFS'],
      langsISpeak: ['English', 'German', 'Croatian'],
      cv_langs: [
        {text: 'English', value: 'en'},
        {text: 'German', value: 'de'},
        {text: 'Croatian', value: 'hr'}
      ],
      cv_lang: 'en'
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
    },
    viewCV () {
      this.$refs.cvModal.close()
      window.open(cvEn)
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
  top: 45%;
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

.about-footer{
  margin-top:80px;
  text-align:center;
}
.cv-btn:active, .cv-btn:focus{
  color: #14151a !important
}

.close-modal-cv i{
    font-size: 30px;
}
.close-modal-cv {
    color: #777;
    position: absolute;
    top: 12px;
    right: 0
}
.close-modal-cv:hover {
    color: #eee !important;
}

.modal-title-cv{
    font-weight: 300;
    margin-top: 40px;
    margin-bottom: 20px;
}
.info-divider{
    width: 200px;
    border: 0; 
    height: 1px; 
    background-image: linear-gradient(to right, rgba(20, 20, 25, 0), rgba(50, 50, 55, 0.75), rgba(20, 20, 25, 0));
    margin-bottom: 30px;
}
.cv-list{
    border:none;
    padding-left:30px
}

.cv-confirm-btn{
  margin-top: 50px
}
.cv-modal-layout{
  margin: 0
}
</style>
