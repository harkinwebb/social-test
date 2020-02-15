<template>
  <div class="social-list">
    <card v-for="post in postArray" :key="post.title" :card-data=post ></card>
  </div>
</template>

<script>
import Card from '@/components/Card.vue'
import TwitterData from '@/assets/twitterData'
import axios from 'axios' 

export default {
  name: 'SocialList',
  components: {
    Card
  },
  props: {
    msg: String
  },
  data: function(){
      return{
        loaded: false,
        postArray: [],
      }
  },
  mounted(){
    this.getComponentData()
  },
  methods:{
    getComponentData: function(){
      axios.defaults.crossDomain = true
      axios.defaults.withCredentials = true

      this.loaded = false

      let youTubeUrl = new URL('https://www.googleapis.com/youtube/v3/activities')
      youTubeUrl.searchParams.set('part','snippet')
      youTubeUrl.searchParams.set('channelId','UCGkRPUvp4tZXyd4EZUdjrCw')
      youTubeUrl.searchParams.set('key','AIzaSyC6H-od890sW_0HxzNqjo3fY3cCQhEcR6Y')

      axios
        .get(youTubeUrl.href)
        .then(response => {
          let itemArray = response.data.items
           
          itemArray.forEach(item => {
            let socialItemObj = {}

            socialItemObj.title = item.snippet.title
            socialItemObj.description = item.snippet.description
            socialItemObj.published = item.snippet.publishedAt
            socialItemObj.source = "youTube"
            //TODO: Add Thumb Info

            this.postArray.push(socialItemObj)
          })
          
        })
        .catch(error => {
          console.log(error)
        })

        TwitterData.forEach(twitterItem => {
          let socialItemObj = {}

            socialItemObj.title = ''
            socialItemObj.description = twitterItem.text
            socialItemObj.published = twitterItem.created_at
            socialItemObj.source = "twitter"
            //TODO: Add Thumb Info

            this.postArray.push(socialItemObj)
        })
      
      /*
      Benching this for now, this should be called to refresh the Bearer Token incase it has been invalidadted and the timeline called with the reurned token, This works in Postman 
      but I get a CORS preflight from the browser. I'm sure this is fixable but for the sake of time I'm moving on.
      */

     /*
      let twitterTokenUrl = new URL('https://api.twitter.com/oauth2/token')
      twitterTokenUrl.searchParams.set('grant_type','client_credentials')
      const config = {
        headers: { 
          "Authorization": `Basic TzlHWHFadzBrTGlnazZyY3cyU3VwOW1tdTpqRjgzVTUzYVBrTkJCbXFFUGRpWGlhNmZkMW9zV2JqUFJvODRVR1B6bWZESTZ6NUhxSA==`,
          "Content-Type": "application/x-www-form-urlencoded"
        }
      }
      const bodyParameters = {}
      
      axios
        .post( 
          twitterTokenUrl.href,
          bodyParameters,
          config
        )
        .then(console.log)
        .catch(console.log) 
      
       
      let twitterUrl = new URL('https://api.twitter.com/1.1/statuses/user_timeline.json')
      twitterUrl.searchParams.set('screen_name','Framestore')
      twitterUrl.searchParams.set('count','10')
      
      axios
        .get(
          twitterUrl.href,
          {
            headers: { 
              "Authorization": "Bearer AAAAAAAAAAAAAAAAAAAAAFMPCgEAAAAAgfFcO8vrwqxrJwHu2LKmdqdm8LA%3DMk2LZ9XkCx3e1d7uTE56Ygkk53L9lH0VdolMWZTqyy4Uc4Smoq",
              "Content-Type": "application/x-www-form-urlencoded"
            }
          }
        )
        .then(response => {
          console.log(response)
        })
        .catch(error => {
          console.log(error)
        })
    */
    }
  },
}
</script>

<style scoped lang="scss">

</style>