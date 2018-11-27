<template>
  <v-layout column justify-center align-center>
    <v-flex xs12 sm8 md6>
      <div class="text-xs-center">
        <logo/>
        <vuetify-logo/>
      </div>
      <v-card>
        <v-card-title class="headline">Welcome to the Vuetify + Nuxt.js template</v-card-title>
        <v-card-text>
          <p>Username:{{user.Username}}</p>
          <p>Password:{{user.Password}}</p>
  
          <div v-for="(item, key) in object" :key="key">
            PlayerName:{{item.PlayerName}}
          </div>
        </v-card-text>
        <v-card-actions>
          <v-spacer/>
          <v-btn color="primary" flat nuxt to="/inspire">Continue</v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
  import axios from 'axios';
  import Logo from '~/components/Logo.vue'
  import VuetifyLogo from '~/components/VuetifyLogo.vue'
  
  export default {
    components: {
      Logo,
      VuetifyLogo
    },
    data() {
      return {
        object: {}
      }
    },
    mounted() {
      this.getObject()
    },
    async asyncData({error,req}) {
      console.log('req:'+req);
      
      let baseUrl=req&&'http://localhost:8080'||'';
      let {
        data
      } = await axios.get(baseUrl+'/v1/user/user_11111')
      return {
        user: data
      }
      try {
        
      } catch (err) {
        if(err.response.status===404){
          error({ statusCode: 404, message: 'Post not found' })
        }else{
          error({ statusCode: 500, message: '服务器错误' })
        }
      }
    },
    methods: {
      async getObject() {
        
        try {
          let {
          data
        } = await axios.get('/v1/object')
        this.object = data;

        } catch (err) {
          console.log("1111111111:"+err.response);
          
        }
      }
    }
  }
</script>
