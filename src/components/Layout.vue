<template>
  <q-layout>

    <div class="layout-view">

      <div class="text-center nav">
        <router-link class="nav-link" 
            v-for="item in menu" 
            v-if="item.link != $route.fullPath" 
            :to="item.link">
          <span>{{item.text}}</span>
        </router-link>
      </div>
      
    </div>

    <button class="contact-info-btn grey clear circular" 
            style="font-weight:400"
            @click="$refs.infoModal.open()">
        <i>person</i>
        <q-tooltip anchor="center left" self="center right" :offset="[-10,0]">
            Contact info 
        </q-tooltip>
    </button>

    <q-modal ref="infoModal" class="maximized">
        <q-layout>
            <div slot="header" class="toolbar">
                <button @click="$refs.layoutModal.close()">
                    <i>keyboard_arrow_left</i>
                </button>
                <q-toolbar-title :padding="1">
                    Header
                </q-toolbar-title>
            </div>
                <div slot="header" class="toolbar primary">
                <q-search class="primary"></q-search>
            </div>
            <div slot="footer" class="toolbar">
                <q-toolbar-title :padding="1">
                    Footer
                </q-toolbar-title>
            </div>
            <div class="layout-view">
                <div class="layout-padding">
                    <h1>Modal</h1>
                    <button class="primary" @click="$refs.infoModal.close()">Close</button>
                    <p class="caption" v-for="n in 15">This is a Modal presenting a Layout.</p>
                </div>
            </div>
        </q-layout>
    </q-modal>

  </q-layout>
</template>

<script>
export default {
  data () {
    return {
      menu: [
        {text: 'Home', link: '/'},
        {text: 'About', link: '/about'},
        {text: 'Portfolio', link: '/portfolio'},
        {text: 'Contact', link: '/contact'}
      ]
    }
  }
}
</script>

<style scoped>
.nav-link {
    color: #bbb;
    font-weight: 300;
    display: inline-block;
    padding: 30px 10px 10px 10px;
    text-transform: uppercase;
    text-shadow: 0px 5px 10px #050505;
    -webkit-text-shadow: 0px 5px 10px #050505;
    -moz-text-shadow: 0px 5px 10px #050505;
    transition: 0.40s all ease;
}
.nav-link:hover {
    color: #eee;
}

@media screen and (min-width: 600px) {
    .nav-link {
        padding-left: 50px;
        padding-right: 50px
    }
}
@media screen and (min-width: 1000px) {
    .nav-link {
        padding-left: 100px;
        padding-right: 100px
    }
}

.contact-info-btn {
    position: absolute;
    bottom: 15px;
    right: 15px;
}
.contact-info-btn i{
    font-size: 26px;
}
</style>
