<template>
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md6>
            <v-card class="elevation-4">
              <v-form @submit.prevent="login">
              <v-toolbar dark>
                <v-toolbar-title>Login form</v-toolbar-title>
              </v-toolbar>
              <v-card-text>
                <p v-if="this.$route.params.registered">Successfully Registered, Sign In Below</p>
                  <v-text-field v-model="form.email" prepend-icon="alternate_email" name="email" label="Email" type="text"></v-text-field>
                  <v-text-field v-model="form.password" id="password" prepend-icon="lock" name="password" label="Password" type="password"></v-text-field>
                  <p class="error-msg">{{errors[0]}}</p>

              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn type="submit" color="primary">Login</v-btn>
              </v-card-actions>
              </v-form>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
</template>

<script>
export default {
  data() {
    return {
      form: {
        email: null,
        password: null
      },
      errors: []
    }
  },
  methods: {
    async login() {
      await this.$auth.loginWith("local", {
        data: this.form
      }).then(dat => {
        this.$router.push('/')
      }).catch(err => {
        this.errors.unshift(err.response.data.error)
      })


    }
  }
}
</script>

<style>

</style>
