<template>
  <v-layout row wrap  dark justify-space-between>
    <v-flex xs12  md6 lg3>
      <v-card>
        <v-card class="blue-img">
            <v-btn
              absolute
              dark
              fab
              bottom
              left
              color="pink"
              icon
            >
              <v-avatar size="55"><img src="https://banner2.kisspng.com/20180703/ya/kisspng-computer-icons-user-avatar-user-5b3bafe2381423.1933594815306383062297.jpg"  alt=""></v-avatar>
            </v-btn>
        </v-card>
        <v-layout row wrap bottom>

        </v-layout>
        <v-card-title primary-title>
          <v-layout row >
            <v-flex xs3>
              <v-layout column mt-3>
                <v-layout row wrap justify-left>
                  Tweets
                </v-layout>
                <v-layout row wrap class="blue--text headline" justify-left>
                  {{tweetCount}}
                </v-layout>
              </v-layout>
            </v-flex>
          </v-layout>

        </v-card-title>
      </v-card>
    </v-flex>


    <v-flex xs12 md5>
      <addTweet/>
     <v-card v-for="(tweet, index) in tweets" :key="index">
       <v-card-title primary-title>
         <nuxt-link :to="`/user/${tweet.user}`">{{tweet.user}}</nuxt-link> -{{tweet.posted}}
       </v-card-title>
        <v-card-text>
          {{tweet.tweet}}
        </v-card-text>
     </v-card>
    </v-flex>
    <v-flex xs12 md3>
      hello
    </v-flex>
  </v-layout>
</template>

<script>

import addTweet from '@/components/addTweet'
import axios from 'axios'

export default {
  middleware: 'auth',


  data() {
    return {
      tweets: [],
      tweetCount: null
    }
  },

  components: {
    addTweet
  },
  mounted() {
    this.$axios.$get('http://nuxtbackend.test/api/auth/tweet').then(dat => {
      this.tweets = dat.data;
    })
    this.$axios.$get('http://nuxtbackend.test/api/auth/userdetails').then(dat => {
      this.tweetCount = dat;
    })
  }
}
</script>
<style>
.blue-img {
  width: 100%;
  height: 8rem;
  background:#1DA1F2!important;
}

</style>
