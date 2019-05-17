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

                  <v-text-field v-model="form.email" prepend-icon="alternate_email" name="email" label="Email" type="text"></v-text-field>
                  <p class="error-msg">Error message</p>
                  <v-text-field v-model="form.password" id="password" prepend-icon="lock" name="password" label="Password" type="password"></v-text-field>
                  <p class="error-msg">Error message</p>

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
      }
    }
  },
  methods: {
    async login() {
      await this.$auth.loginWith("local", {
        data: this.form
      }).then(dat => {
        console.log(dat)
      })

      this.$router.push('/')
    }
  }
}
</script>

<style>

</style>
