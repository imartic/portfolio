<template>
  <!-- Don't drop "q-app" class -->
  <div id="q-app">

    <Layout></Layout>
    <transition name="fade">
      <router-view></router-view>
    </transition>

  </div>
</template>

<script>
import Layout from './components/Layout'

export default {
  components: {
    Layout
  }
}
</script>

<style>
html {
	overflow-x: hidden;
}
body{
  background: #14151a;
  color: #bbb;
}

.layout-padding, .logo{
  margin-bottom: 40px
}

button{
  border-radius: 0
}
button:hover{
  color: #14151a !important
}

.fade-enter-active, .fade-leave-active {
  transition-property: opacity;
  transition-duration: .25s;
}
.fade-enter-active {
  transition-delay: .25s;
}
.fade-enter, .fade-leave-active {
  opacity: 0
}

@media screen and (max-height: 600px) {
  .layout-padding, .logo{
    margin-top: 60px
  }
}
@media screen and (max-width: 400px) {
  .layout-padding, .logo{
    margin-top: 20px
  }
}
</style>
