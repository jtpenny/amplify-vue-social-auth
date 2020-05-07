<template>
  <div>Continuing to sign you in....</div>
</template>

<script>
import Vue from 'vue';
import Amplify, * as AmplifyModules from 'aws-amplify';
import { AmplifyEventBus } from 'aws-amplify-vue'

let AmplifyStore = AmplifyModules.Auth._AmplifyStore

export default {
  name: 'Callback',
  data () {
    return {
      signedIn: false
    }
  },
 beforeCreate() {

AmplifyModules.Hub.listen('auth', (data) => {
  console.log({"SIGNIN" : data})
  
  if(data.payload.event=='signIn') {
    this.$router.push({path: '/'})
  }
});
  
  },
  
}
</script>