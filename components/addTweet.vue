<template>
     <v-card>
       <v-form @submit.prevent="submitTweet">
         <v-text-field
          v-model="tweetInput"
           name="tweetInput"
           label="What's happening?"
           id="id" class="ml-3 mr-3"
           autocomplete="off"
         ></v-text-field>
         <v-layout row wrap justify-end>
           <v-btn type="submit" dark color="blue lighten-1">Submit</v-btn>
         </v-layout>

       </v-form>
     </v-card>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      tweetInput: null,
      tags: []
    }
  },

  methods: {
    async submitTweet(tweet){
      this.tags.push(this.tweetInput.match(/#\S+/g))
      await this.$axios.$post('http://nuxtbackend.test/api/auth/tweet', {
        tweet: this.tweetInput,
        userId: this.user.username,
        tags: this.tags

      }).then(dat => {
        this.tags = []
        console.log(dat)
            this.$axios.$get('http://nuxtbackend.test/api/auth/tweet').then(dat => {
      this.$parent.tweets = dat.data;
              this.$parent.tweetCount++
        this.tweetInput = null
            });
      })
    }
  }
}
</script>
<style>

</style>
