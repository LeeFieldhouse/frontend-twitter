<template>
     <v-card>
       <v-form>
         <v-text-field
          v-model="tweetInput"
           name="tweetInput"
           label="What's happening?"
           id="id" class="ml-3 mr-3"
         ></v-text-field>
       </v-form>
     </v-card>
</template>

<script>
import axios from 'axios'
export default {
  data() {
    return {
      tweetInput: null
    }
  }
}
</script>
<style>

</style>
