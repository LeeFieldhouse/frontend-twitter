<template>
  <v-app>
    <navbar/>
    <v-content>

        <nuxt />

    </v-content>

    <v-footer
      :fixed="fixed"
      app
    >
      <span>&copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
import navbar from '@/components/navbar'
export default {
  components: {
    navbar
  },
  data() {
    return {

      fixed: true,
      title: 'Vuetify.js'
    }
  }
}
</script>
<style>

html {
font-size: 62.5%;
}

body {
  font-size: 2rem;
}

.error-msg {
  margin-top: -1rem;
  margin-left: 2.3rem;
  color: red;
}

</style>
