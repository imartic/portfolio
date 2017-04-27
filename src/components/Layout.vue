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
            @click="$refs.infoModal.toggle()">
        <i>person</i>
        <q-tooltip anchor="center left" self="center right" :offset="[-10,0]">
            Contact info 
        </q-tooltip>
    </button>

    <q-modal ref="infoModal" class="full-modal maximized">
        <q-layout>

            <div class="layout-view">
                <button class="close-modal text-shadow" @click="$refs.infoModal.toggle()">
                    <i>close</i>
                </button>
                <div class="layout-padding text-center">
                    <h4 class="modal-title text-shadow">Contact information</h4>
                    <hr class="info-divider"/>
                    <ul class="contact-info" v-for="item in contactInfo">
                        <li>
                            <a v-if="item.link !== null" :href="item.link" v-bind:class="{ 'no-pointer-events': checkLink(item.link)}">
                                <span class="title text-shadow" v-if="item.fa == null"><i>{{item.icon}}</i></span>
                                <span class="title text-shadow" v-else><i :class="item.icon"></i></span>
                                <span class="text text-shadow">{{item.text}}</span>
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
        /* {text: 'imartic.github.io', icon: 'language', link: 'https://imartic.github.io'}, */
        {text: '+385 91 200 8778', icon: 'phone'},
        {text: 'imartic14', icon: 'fa fa-skype', fa: 'sykpe'},
        {text: 'LinkedIn profile', icon: 'fa fa-linkedin', fa: 'linkedin', link: 'https://www.linkedin.com/in/ivan-martić-81b7a9a5'},
        {text: 'GitHub profile', icon: 'fa fa-github', fa: 'github', link: 'https://www.github.com/imartic'}
      ]
    }
  },
  methods: {
    checkLink (link) {
      return link == null
    }
  }
}
</script>

<style>
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
    position: fixed;
    bottom: 15px;
    right: 15px;
}
.contact-info-btn i{
    font-size: 26px;
}

.full-modal{
    opacity: 0.97;
    filter: alpha(opacity=97);
}
.full-modal .layout-view{
    border: 1px solid rgba(100,105,120,0.4);
    border-radius: 0;
    background-color: #14151a;
}

.close-modal i{
    font-size: 38px;
}
.close-modal {
    color: #777;
    position: fixed;
    bottom: 22px;
    right: 8px
}
.close-modal:hover {
    color: #eee !important;
}

.modal-title{
    font-weight: 300;
    margin-top: 70px;
    margin-bottom: 60px;
}

@media screen and (max-width: 600px) {
    .modal-title {
        font-size: 25px;
        margin-top: 50px;
        margin-bottom: 40px;
    }
}

.info-divider{
    width: 200px;
    border: 0; 
    height: 1px; 
    background-image: linear-gradient(to right, rgba(20, 20, 25, 0), rgba(50, 50, 55, 0.75), rgba(20, 20, 25, 0));
    margin-bottom: 60px;
}

.text-shadow{
    text-shadow: 0px 5px 10px #050505;
    -webkit-text-shadow: 0px 5px 10px #050505;
    -moz-text-shadow: 0px 5px 10px #050505;
}

.contact-info{list-style-type: none;padding:0}
.contact-info li{padding-bottom:8px}
.contact-info .title{color:#ddd;display:inline-flex;vertical-align:middle;padding-bottom:4px}
.contact-info .title i{font-size:28px;padding-right:15px}
.contact-info .title .fa{padding-left:2px;}
.contact-info .text{
    font-size:20px;
    font-weight:300;
    line-height:20px;
    color:#bbb;
    -webkit-transition: all .4s;
    -moz-transition: all .4s;
    transition: all .4s;
}
.contact-info i{font-size:28px;padding-right:5px;color:#bbb}
.contact-info .fa{padding-left:3px;}
.contact-info .text:hover{
    color: #eee
}
</style>
