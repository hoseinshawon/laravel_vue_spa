<template>
  <v-content>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn @click="logout" v-if="loggedIn">
        Logout
      </v-btn>
    </v-app-bar>

    <v-content>
      <router-view></router-view>
    </v-content>
  </v-content>
</template>

<script>

export default {
  name: 'App',
  data: () => ({
    //loggedIn: false
  }),


  created(){
    return new Promise((resolve) => {
      if(localStorage.getItem('token')){
        this.loggedIn = true;
        resolve(true);
      }
      else{
        this.loggedIn = false;
        resolve(false);
      }
    });
  },


  methods: {

      logout(){
        return new Promise((resolve) => {
            localStorage.removeItem('token');
            resolve(true);
        })
        .then(() => {
          this.$router.push({name: 'login'});
        })
      },






/*
      setLoggedInState(){
        return new Promise((resolve) => {
            if(localStorage.getItem('token')){
                this.loggedIn = true;
                resolve(true)
            }
            else{
                this.loggedIn = false;
                resolve(false)
            }
        });
      }
*/



  }
};
</script>



