<template>
  <div>
        <v-navigation-drawer
      v-model="drawer"
  class="side-bar"
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
          :to="`/users/${user.username}`"
          router
          exact
          class="sidebar-avatar"
        >
          <v-list-tile-action >
            <v-avatar
              size="60"

            >
              <img :src="`${user.avatar}`" alt="alt">
            </v-avatar>
          </v-list-tile-action>

        </v-list-tile>

        <v-list-tile @click.prevent="logOut">
          <v-list-tile-action >
            <v-icon size="48">home</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            Home
          </v-list-tile-content>
        </v-list-tile>

        <v-list-tile @click.prevent="logOut">
          <v-list-tile-action >
            <v-icon size="38">person</v-icon>
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
  z-index: 9!important;
}

.nav-logo {
  max-height: 100%;
  max-width: 100%;
}

.side-bar{
  z-index: 10!important;
}

.v-toolbar__content .v-btn--icon {
  color: white!important;
}

.sidebar-avatar{
  display: flex;
  flex-direction: row;
  justify-content: center;
  width: 100%!important;
}
.sidebar-avatar:hover{
  background: none!important;
}




</style>
