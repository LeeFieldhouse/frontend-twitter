<template>
<v-layout row wrap v-if="userProfile">
  <!-- start header section -->
  <v-flex xs12>
      <v-card>
        <v-card class="blue" height="17.5rem">
            <v-btn
              absolute
              dark
              fab
              bottom
              left
              icon
              class="ml-5 mb-5 pb-5 profile-av"
            >
              <v-avatar class="" size="15rem"><img :src="`${userProfile.user.avatar}`"  alt=""></v-avatar>
            </v-btn>
        </v-card>
        <v-layout row wrap bottom>
          <v-flex xs12>
            <v-card flat class="header-profile title text-xs-center font-weight-bold grey--text text--darken-2" color="white" height="6rem" >
                <v-layout row wrap>
                  <v-flex xs4 md2 lg1>
                    <v-layout column >
                      <v-flex xs1 >
                        Tweets
                      </v-flex>
                      <v-flex xs1>
                        {{userProfile.user.tweet_count}}
                      </v-flex>
                    </v-layout>
                  </v-flex>
                  <v-flex xs4 md2 lg1>
                    <v-layout column >
                      <v-flex xs1 >
                        Likes
                      </v-flex>
                      <v-flex xs1>
                        {{userProfile.likes}}
                      </v-flex>
                    </v-layout>
                  </v-flex>
                </v-layout>
            </v-card>
          </v-flex>
        </v-layout>
      </v-card>
    </v-flex>
    <!-- end header section -->
    <v-container>
      <v-layout row wrap justify-space-between>
      <v-flex xs12 sm4 md3>
        <v-card >
          <v-card-title class="blue lighten-2 white--text headline font-weight-bold">
            Favourite Hashtags
          </v-card-title>
          <v-card-text >
            <div v-for="(fav_tag, index) in userProfile.fav_tags" :key="index">
              {{fav_tag.tag}}
            </div>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex xs12 sm4 md3>
        <v-card >
          <v-card-title class="blue lighten-2 white--text headline font-weight-bold">
            Most Popular Tweets
          </v-card-title>
          <v-card-text >
            <v-card v-for="(pop_tweet, index) in userProfile.pop_tweets" :key="index">
              {{pop_tweet}}
            </v-card>
          </v-card-text>
        </v-card>
      </v-flex>
      <v-flex xs12 sm4 md3>
        Yooo
      </v-flex>
      </v-layout>

    </v-container>
  </v-layout>
</template>

<script>
import axios from 'axios'
export default {

  data() {
    return {
      userProfile: null,
      tweetCount: null,

    }
  },
beforeCreate(){
     this.$axios.$get(`auth/users/${this.$route.params.id}`).then(dat => {
        if(dat === "Doesn't Exist"){
         this.$router.go(-1)
        }else{
          console.log(dat.pop_tweets)
          this.userProfile = dat
        }
      })
  }


}
</script>

<style>
.header-profile {
  display: flex;
  flex-direction: row;
  align-items: center;
  padding-left: 20rem;
}

.profile-av {
  z-index: 1!important;
}
</style>
