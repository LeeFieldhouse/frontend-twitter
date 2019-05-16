<template>
  <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md6>
            <v-card class="elevation-4">
              <v-toolbar dark>
                <v-toolbar-title>Register form</v-toolbar-title>
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field v-model="data.name" prepend-icon="person" name="name" label="Name" type="text"></v-text-field>
                  <v-text-field v-model="data.email" prepend-icon="alternate_email" name="email" label="Email" type="text"></v-text-field>
                  <v-text-field v-model="data.password" id="password" prepend-icon="lock" name="password" label="Password" type="password"></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="primary">Register</v-btn>
              </v-card-actions>
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
      data: {
        name: null,
        email: null,
        password: null,
      }
    }
  }
}
</script>

<style>

</style>
