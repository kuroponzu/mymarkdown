<template>
  <div id="app">
    <Home v-if="!isLogin"></Home>
    <Editor v-if="isLogin" :user="userData"></Editor>
  </div>
</template>

<script>
import Home from "./components/Home.vue";
import Editor from "./components/Editor.vue";
import Vue from "vue";
Vue.config.devtools = true;

export default {
  name: "app",
  data() {
    return {
      isLogin: false,
      userData: null
    };
  },

  mounted: function() {
    firebase.auth().onAuthStateChanged(user => {
      console.log(user);
      if (user) {
        this.isLogin = true;
        this.userData = user;
      } else {
        this.isLogin = false;
        this.userData = nill;
      }
    });
  },

  components: {
    Home: Home,
    Editor: Editor
  }
};
</script>