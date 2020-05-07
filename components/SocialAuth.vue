<template>
<div class="container">
    <amplify-authenticator />
    <div v-for="social_button in social_buttons" v-bind:key="social_button" class="col-md-3 socialButton">
        <button v-bind:class="'btn btn-block btn-social btn-'+social_button.toLowerCase()" v-on:click="FSI(social_button)" >
          <i v-bind:class="'fa fa-'+social_button.toLowerCase()"></i> 
          Sign in with {{social_button}} 
        </button>
  </div>
</div>
</template>

<style scoped>
.socialButton {
  margin-right: auto;
  margin-left: auto;
  display: block;
  margin-top: 10px;
}
</style>

<script>

import   {components }   from 'aws-amplify-vue';
import { Auth, Hub } from 'aws-amplify';

import BootstrapVue from 'bootstrap-vue'
import 'bootstrap/dist/css/bootstrap.css'
import 'bootstrap-vue/dist/bootstrap-vue.css'

import 'bootstrap-social/bootstrap-social.css'
import 'font-awesome/css/font-awesome.css'

export default {
  data: function () {
    return {
    }
  },
  computed: {
      social_buttons: function() {
          try {
              if(Array.isArray(Auth._config.oauth.socialProviders)) {
                  return Auth._config.oauth.socialProviders;
              }
          }
          catch(err) {
            
              return []
              
          }
          return []
      }
  },
  mounted() {
    console.log(Auth)
  },
  methods: {

      FSI: function(p) {
        Auth.federatedSignIn({provider:p});
      },
  },
}
</script>