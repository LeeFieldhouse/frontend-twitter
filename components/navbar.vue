<template>
  <div>
        <v-navigation-drawer
      v-model="drawer"

      fixed
      app
      color="blue"
    >
    <!-- start guest sidebar -->
      <v-list v-if="!loggedIn">
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

      <!-- end guest in sidebar -->

      <!-- start -->
      <v-list v-if="loggedIn">
        <v-list-tile
          to="/"
          router
          exact
          class="sidebar-avatar"
        >
          <v-list-tile-action>
            <v-avatar
              size="48"

            >
              <img :src="`${user.avatar}`" alt="alt">
            </v-avatar>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title class="headling">@{{user.username}}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>

        <v-list-tile @click.prevent="logOut">
          <v-list-tile-action >
            <v-icon size="48">person</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            Logout
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar
      fixed
      app
      color="white--text"
      class="navbar"
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
      // shows not logged in sidebar
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
  },
  methods: {
    logOut() {
      this.$axios.$post('/auth/logout').then(dat => {
        this.$router.go('/login')
      }).catch(err => {
        console.log(err)
      })
    }
  }

}
</script>

<style>
nav {
  background: #659FCB!important;
  z-index: 10!important;
}

.nav-logo {
  max-height: 100%;
  max-width: 100%;
}

.v-toolbar__content .v-btn--icon {
  color: white!important;
}





</style>
