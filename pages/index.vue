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
              icon
            >
              <v-avatar size="55"><img :src="`${user.avatar}`"  alt=""></v-avatar>
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
      <v-card>

        <v-card-title primary-title>
          <v-layout row >
            <v-flex xs3>
              <v-layout column mt-3>
                <v-layout row wrap justify-left>
                  Trending #
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
      <addTweet class="mb-1"/>
     <v-card v-for="(tweet, index) in tweets" :key="index" class="mb-1">
       <v-layout row>
         <v-flex xs2>
           <div class="text-xs-center pt-4">
              <v-avatar size="48"><img :src="`${tweet.user.avatar}`"  alt=""></v-avatar>
           </div>

         </v-flex>
         <v-flex xs9>
       <v-card-title primary-title>
         <nuxt-link :to="`/user/${tweet.user.username}`">{{tweet.user.username}}</nuxt-link> -{{tweet.posted}}
       </v-card-title>
        <v-card-text>
          {{tweet.tweet}}
          <v-layout row class="mt-2">
            <v-icon  @click="likeTweet(tweet.id)" class=" mr-1" :class="tweet.liked ? 'blue--text' : 'grey--text'">thumb_up_alt</v-icon>
            <div class="font-weight-medium">{{tweet.likes}}</div>
          </v-layout>
        </v-card-text>
         </v-flex>
         <v-flex xs1 v-if="user.username === tweet.user.username">
           <div class="text-xs-center">
             <v-icon class="icon" size="1rem" @click="deleteTweet(tweet.id)">delete</v-icon>
           </div>
         </v-flex>
       </v-layout>

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
  methods: {
    deleteTweet(id) {
      this.$axios.$delete(`auth/tweet/${id}`, {
        id: id
      }).then(dat => {
        this.tweetCount--
        this.tweets = this.tweets.filter(tweet => {
          return tweet.id !== id
        })
      })
    },

    likeTweet(id) {
      this.$axios.$post(`auth/tweet/like/${id}`).then(dat => {
        this.$axios.$get('auth/tweet').then(dat => {
          this.tweets = dat.data
        })
      })
    }
  },

  mounted() {
    this.$axios.$get('auth/tweet').then(dat => {
      this.tweets = dat.data;
    })
    this.$axios.$get('auth/userdetails').then(dat => {
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

.icon {
  cursor: pointer;
}

</style>
