<template>

  <div class="logo-container non-selectable">       
    <div class="logo" :style="position">
      
      <div class="home-title">Contact me</div>
      <div class="home-subtitle">
        
        <form name="mail" class="mail-frm" action="https://formspree.io/ivan.martic.ri@gmail.com"
              method="POST">

          <div class="row wrap gutter">
            <div class="auto">
              <input type="email" class="full-width" v-model="mail" placeholder="Your e-mail" name="email">
            </div>
            <div class="auto">
              <input class="full-width" v-model="subject" placeholder="Subject" name="_subject">
            </div>
          </div>

          <textarea rows="7" class="full-width" v-model="message" placeholder="Your message" name="message">
          </textarea>

          <input type="hidden" name="_next" value="" />
          <input type="text" name="_gotcha" style="display:none" />

          <transition name="fade">
            <div v-if="alert" class='input-alert'>
              <span class="close-alert" @click="closeAlert()">&times;</span> 
              {{ alertMsg }}
            </div>
          </transition>

          <button type="button" class="grey outline send-btn" @click="sendMail()">
            Send mail
            <i class="on-right">send</i>
          </button>
        </form>

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
      mail: '',
      subject: '',
      message: '',
      alert: false,
      alertMsg: ''
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
    sendMail () {
      if ((document.mail.email.value === '') || (!this.validateEmail(document.mail.email.value))) {
        this.alert = true
        this.alertMsg = 'Please enter a valid e-mail address!'
        document.mail.email.focus()
        return
      }
      if (document.mail._subject.value === '') {
        this.alert = true
        this.alertMsg = 'Please enter a subject!'
        document.mail._subject.focus()
        return
      }
      if (document.mail.message.value === '') {
        this.alert = true
        this.alertMsg = 'Please enter your message!'
        document.mail.message.focus()
        return
      }

      this.alert = false
      this.alertMsg = ''
      document.mail.submit()
    },
    validateEmail (email) {
      var re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
      return re.test(email)
    },
    closeAlert () {
      this.alert = false
      this.alertMsg = ''
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

input, textarea{
  color: #ddd;
  font-weight: 300;
  border: 1px solid #999;
  padding-left: 10px
}
input:hover, textarea:hover, 
input:active, textarea:active,
input:focus, textarea:focus{
  border: 1px solid #eee;
}

.send-btn{
  margin-top: 25px;
}

.input-alert {
  text-shadow: none;
  border: 2px solid #822;
  padding: 18px;
  color: #bbb;
  font-size: 15px;
  margin-top: 20px;
}
.close-alert {
  margin-left: 15px;
  color: #bbb;
  font-weight: bold;
  float: right;
  font-size: 22px;
  line-height: 20px;
  cursor: pointer;
  transition: 0.3s;
}
.close-alert:hover {
  color: #822;
}

.fade-enter-active, .fade-leave-active {
  transition-property: opacity;
  transition-duration: .15s;
}
.fade-enter-active {
  transition-delay: .15s;
}
.fade-enter, .fade-leave-active {
  opacity: 0
}
</style>
