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

    <q-modal ref="infoModal" class="full-modal maximized">
        <q-layout>

            <div class="layout-view">
                <button class="close-modal" @click="$refs.infoModal.close()">
                    <i>close</i>
                </button>
                <div class="layout-padding text-center">
                    <h4 class="modal-title">Contact information</h4>
                    <ul class="contact-info" v-for="item in contactInfo">
                        <li>
                            <a v-if="item.link !== null" :href="item.link">
                                <span class="title" v-if="item.fa == null"><i>{{item.icon}}</i></span>
                                <span class="title" v-else><i :class="item.icon"></i></span>
                                <span class="text">{{item.text}}</span>
                            </a>
                        </li>
                    </ul>
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
      ],
      contactInfo: [
        {text: 'ivan.martic.ri@gmail.com', icon: 'mail', link: 'mailto:ivan.martic.ri@gmail.com?Subject=Hello!'},
        {text: 'imartic.github.io', icon: 'language', link: 'https://imartic.github.io'},
        {text: '+385 91 200 8778', icon: 'phone'},
        {text: 'imartic14', icon: 'fa fa-skype', fa: 'sykpe'},
        {text: 'LinkedIn profile', icon: 'fa fa-linkedin', fa: 'linkedin', link: 'https://www.linkedin.com/in/ivan-martić-81b7a9a5'},
        {text: 'GitHub profile', icon: 'fa fa-github', fa: 'github', link: 'https://www.github.com/imartic'}
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

.full-modal{
    opacity: 0.9;
    filter: alpha(opacity=90);
}
.full-modal .layout-view{
    background-color: #14151a;
}

.close-modal i{
    font-size: 30px
}
.close-modal {
    color: #bbb;
    position: absolute;
    top: 15px;
    right: 15px
}
.close-modal:hover {
    color: #eee !important;
}

.modal-title{
    font-weight: 300;
    margin-top: 70px;
    margin-bottom: 50px
}

.contact-info{list-style-type: none;padding:0}
.contact-info li{padding-bottom:8px}
.contact-info .title{color:#fff;display:inline-flex;vertical-align:middle;padding-bottom:4px}
.contact-info .title i{font-size:23px;padding-right:5px}
.contact-info .title .fa{padding-left:2px;}
.contact-info .text{font-size:16px;font-weight:400;line-height:20px;color:#fff;}
i{font-size:23px;padding-right:5px}
.fa{padding-left:3px;}
</style>
