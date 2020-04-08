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
                <v-toolbar-title>Forgot Password</v-toolbar-title>
                <v-spacer />
                
              </v-toolbar>
              <v-card-text>
                <v-form ref="forgotPasswordForm">
                  <v-text-field
                    label="Email"
                    name="email"
                    type="email"
                    v-model="email"
                  />
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer />
                <v-btn color="primary" @click="sendForgotPassword">Send Email</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>

      <v-snackbar
      v-model="snackbar.show"
    >
      {{ snackbar.text }}
      <v-btn
        color="pink"
        text
        @click="snackbar.show = false"
      >
        Close
      </v-btn>
    </v-snackbar>

        <!--<router-link :to="{name: 'register'}">Register</router-link>-->
    </div>
</template>

<script>

import axios from 'axios';

export default {
    name: "ForgotPassword",
    data(){
      return {
        email: '',
        snackbar: {
            text: '',
            show: false
        }
      }
    },

    methods: {


      sendForgotPassword(){
          if(this.$refs.forgotPasswordForm.validate()){
            return new Promise((resolve, reject) => {
                axios.post('http://127.0.0.1:8000/api/forgot-password', {email: this.email})
                .then((response) => {
                    this.snackbar = {
                        text: 'Email Sent!',
                        show: true
                    };
                    resolve(response);
                })
                .catch((error) => {
                    this.snackbar = {
                        text: 'Failed to Sent Email!',
                        show: true
                    };
                    reject(error);
                });
            });
          }
      }
    }
}
</script>


<style scoped>

</style>