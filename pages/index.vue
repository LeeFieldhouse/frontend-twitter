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
        <v-layout row wrap>

        </v-layout>
        <v-card-title primary-title>
          title
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
  data() {
    return {
      tweets: [],
    }
  },

  components: {
    addTweet
  },
  mounted() {
    axios.get('http://nuxtbackend.test/api/auth/tweet').then(dat => {

      this.tweets = dat.data;
      console.log(this.tweets)
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
