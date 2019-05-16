<template>
  <div>
        <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      fixed
      app
      color="blue"
    >
      <v-list>
        <v-list-tile
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title" />
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar
      fixed
      app
      color="white--text"
    >
      <v-toolbar-side-icon @click="drawer = !drawer" />

      <v-spacer />
      <img class="nav-logo" src="https://static1.squarespace.com/static/57c5e40db3db2be4194b8bdb/t/5873cac617bffc8caed01666/1483983697650/twitter-logo.png" alt="">
      <v-spacer />

    </v-toolbar>
  </div>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
      miniVariant: true,
      items: [
        {
          icon: 'perm_identity',
          title: 'Login',
          to: '/login'
        },
        {
          icon: 'person_add',
          title: 'Register',
          to: '/register'
        }
      ],

    }

  }

}
</script>

<style>
nav {
  background: #659FCB!important;
}

.nav-logo {
  max-height: 100%;
  max-width: 100%;
}

.v-toolbar__content .v-btn--icon {
  color: white!important;
}

</style>
