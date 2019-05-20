<template>
  <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md6>
            <v-card class="elevation-4">
              <v-form @submit.prevent="register">
              <v-toolbar dark>
                <v-toolbar-title>Register form</v-toolbar-title>
              </v-toolbar>
              <v-card-text>
                  <v-text-field v-model.trim="username" prepend-icon="person" name="username" label="Username" type="text"></v-text-field>
                  <v-text-field v-model.trim="email" prepend-icon="alternate_email" name="email" label="Email" type="text"></v-text-field>
                  <v-text-field v-model="password" id="password" prepend-icon="lock" name="password" label="Password" type="password"></v-text-field>
                  <p class="error-msg">Error message</p>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn type="submit" color="primary">Register</v-btn>
              </v-card-actions>
              </v-form>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
        username: null,
        email: null,
        password: null,
    }
  },

  methods: {
    async register(){
      await this.$axios.$post('auth/register', {
        username: this.username,
        email: this.email,
        password: this.password
      })

      // await this.$auth.loginWith("local", {
      //   email: this.email,
      //   password: this.password
      // })

      this.$router.push('/')
    }
  }
}
</script>

<style>

</style>
