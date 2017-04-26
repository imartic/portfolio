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
body{
  background: #14151a;
  color: #bbb;
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
</style>
