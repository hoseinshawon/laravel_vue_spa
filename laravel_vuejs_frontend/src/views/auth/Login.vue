<template>
    <div>
        <v-container
        class="fill-height"
        fluid
      >
        <v-row
          align="center"
          justify="center"
        >
          <v-col
            cols="12"
            sm="8"
            md="4"
          >
            <v-card class="elevation-12">
              <v-toolbar
                color="primary"
                dark
                flat
              >
                <v-toolbar-title>Login form</v-toolbar-title>
                <v-spacer />
                
              </v-toolbar>
              <v-card-text>
                <v-form ref="loginForm">
                  <v-text-field
                    label="Email"
                    name="email"
                    type="email"
                    v-model="user.email"
                  />

                  <v-text-field
                    id="password"
                    label="Password"
                    name="password"
                    type="password"
                    v-model="user.password"
                  />
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer />
                <v-btn color="primary" @click="loginUser">Login</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
        <router-link :to="{name: 'register'}">Register</router-link>
    </div>
</template>

<script>

import axios from 'axios';

export default {
    name: "Login",
    data(){
      return {
        user: {
          email: '',
          password: ''
        }
      }
    },


    /*
    methods: {
      loginUser(){
        if(this.$refs.loginForm.validate()){
          axios.post('http://127.0.0.1:8000/api/login', this.user)
          .then((response) => {    
            localStorage.setItem('token', response.data);
            this.$router.push({name: 'dashboard'});
            //console.log(response.data);
          })
        }
        //console.log(this.user)
      }
    },*/




    methods: {




      loginUser(){
        if(this.$refs.loginForm.validate()){

          return new Promise((resolve, reject) => {
            axios.post('http://127.0.0.1:8000/api/login', this.user)
            .then((response) => {
                if(response.data.access_token){
                    localStorage.setItem('token', response.data.access_token);
                    this.$router.push({name: 'dashboard'});
                    resolve(response);
                }
                //else{
                    //reject(response);
                //}
            })
            .catch((error) => {
                reject(error);
            })
        })

        }
      },









    }



}
</script>


<style scoped>

</style>