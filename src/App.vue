<template>
  <v-app>
    <v-main>
      <v-app-bar
        v-if="!isLoginPage"
        :color="color"
        density="compact"
      >
        <template v-slot:prepend>
          <v-app-bar-nav-icon class="icon_color"></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title id="text_color" class="font-size28">ほんのいちにち</v-app-bar-title>
        <v-btn icon @click="logout" class="icon_color">
          <v-icon>mdi-logout</v-icon>
        </v-btn>

      </v-app-bar>
      <div id="app">
        <router-view/>
      </div>
      <v-bottom-navigation
        v-if="!isLoginPage"
        v-model="value"
        active
        :color="color">
    
        <v-btn @click="this.$router.push('/post')" class="button ">
          <v-icon class="navicon float">mdi-note</v-icon>
          <span class="font-size28 float">投稿</span> 
        </v-btn>
        
        <v-btn @click="this.$router.push('/')" class="button">
          <v-icon class="navicon">mdi-home</v-icon>
          <span class="font-size28">ホーム</span>
        </v-btn>
  
        <v-btn @click="this.$router.push('/setting')" class="button">
          <v-icon class="navicon">mdi-cog</v-icon>
          <span class="font-size28">設定</span>
        </v-btn>
        
      </v-bottom-navigation>
    </v-main>
  </v-app>
</template>
<script>
import {baseUrl} from '@/assets/config.js';
export default {
  name: 'App',

  data: () => ({
    value: parseInt(window.localStorage.getItem('pageIndex')) | null,
  }),
  created() {
    window.localStorage.setItem('pageIndex', 1);
  },
  methods: {
   logout() {
      window.localStorage.clear();
      this.$router.push({name: "Login"});
   }
  },
  computed: {
    isLoginPage() {
      return this.$route.path === '/Login' ;
    },
    color() {
    return "var(--main-color, #4dc4ff)"; // カスタム変数を返す
    },
    currentPath() {
      if(this.$route.path === '/') {
        console.log("aaa")
        return true;
      }
    }
  }
}
</script>

<style scoped>
    #text_color{
      color: #fff
    }
    .font-size28{
    	font-size: 28px;
    }
    .navicon{
        font-size: 35px;
    }
    .float{
       float: left !important;
    }
    .v-bottom-navigation .button {
      width: 130px !important; /* ボタンの横幅を指定 */
    }
    .v-bottom-navigation{
      height:80px !important;
    }
    .icon_color{
      color: #fff;
    }

</style>
