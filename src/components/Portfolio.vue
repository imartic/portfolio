<template>

  <div class="logo-container non-selectable">       
    <div class="logo" :style="position">
      
      <div class="home-title">Portfolio</div>
      <div class="home-subtitle">

      <div class="row wrap gutter sm-column items-stretch">
        <div class="auto lg-width-1of3" v-for="project in portfolio">
          <div class="project-card">
            <div class="card-title">{{ project.title }}</div>

            <div class="card-content tech-section">
              <div v-for="tech in project.tech" class="tech-item">{{ tech }}</div>                            
            </div>

            <div class="card-content project-text">{{ project.text }}</div>
            <div class="card-actions">
              <button v-if="project.github !== ''" 
                class="circular small grey clear" 
                @click="openUrl(project.github)">
                <i class="fa fa-github"></i>
                <q-tooltip anchor="center right" self="center left" :offset="[10,0]">
                  View on GitHub
                </q-tooltip>
              </button>

              <div class="auto"></div>

              <router-link v-if="project.link !== ''" :to="{ name: item.link}">
                <button class="grey clear outline">
                  View project
                </button>
              </router-link>
            </div>

          </div>
        </div>
      </div>
        
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
      rotateX: 0,
      portfolio: [
        {
          title: 'Portfolio site',
          thumbnail: '',
          text: 'This portfolio site was created with Vue.js.',
          tech: ['Vue.js', 'Quasar Framework'],
          github: 'https://github.com/imartic/portfolio',
          link: ''
        },
        {
          title: 'MyBiz v1',
          thumbnail: '',
          text: 'A web application for creating and exporting business proposals.',
          tech: ['C#', 'MS SQL Server', 'JavaScript/jQuery', 'HTML', 'CSS', 'Material Design Lite'],
          github: 'https://github.com/imartic/MyBiz',
          link: ''
        },
        {
          title: 'MyBiz v2',
          thumbnail: '',
          text: 'Upgrade from Version 1. In early phases of development.',
          tech: ['Vue.js', 'Quasar Framework', '...'],
          github: 'https://github.com/imartic/MyBiz-v2',
          link: ''
        },
        {
          title: 'More projects to be included...',
          thumbnail: '',
          text: '',
          tech: [],
          github: '',
          link: ''
        }
      ]
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
    openUrl (url) {
      window.open(url, '_blank').focus()
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
  top: 40%;
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
.project-card .card-content{
  height: 110px
}

.card-actions > *:not(:last-child){
  padding: 0
}

@media screen and (max-width: 1277px) {
  .project-card .card-content{
    height: auto
  }
}
</style>
