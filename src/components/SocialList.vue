<template>
  <div class="social-list">
    <card v-for="post in postArray" :key="post.id" :card-data=post ></card>
  </div>
</template>

<script>
import Card from '@/components/Card.vue'
import TwitterData from '@/assets/twitterData'
import axios from 'axios' 
import moment from 'moment'

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
            let postingDate = moment(item.snippet.publishedAt)
            let today = moment();
            let duration = moment.duration(today.diff(postingDate))
            
            socialItemObj.id = item.id
            socialItemObj.title = item.snippet.title
            socialItemObj.description = item.snippet.description
            socialItemObj.published = postingDate.format('DD/MM/YYYY HH:mm:ss')
            socialItemObj.postAge = Math.round(duration.asDays()) 
            socialItemObj.source = "youTube"
            socialItemObj.image = item.snippet.thumbnails.medium.url

            this.postArray.push(socialItemObj)
          })
          
        })
        .catch(error => {
          console.log(error)
        })

        TwitterData.forEach(twitterItem => {
          let socialItemObj = {}

          let postingDate = moment(twitterItem.created_at, 'ddd MMM DD HH:mm:ss ZZ YYYY')
          let today = moment();
          let duration = moment.duration(today.diff(postingDate))
          
          socialItemObj.id = twitterItem.id
          socialItemObj.title = ''
          socialItemObj.description = twitterItem.text
          socialItemObj.published = postingDate.format('DD/MM/YYYY HH:mm:ss')
          socialItemObj.postAge = Math.round(duration.asDays())
          socialItemObj.source = "twitter"

          
          if(twitterItem.entities.media){
            socialItemObj.image = twitterItem.entities.media[0].media_url_https
          }else{
            socialItemObj.image = ''
          }

          this.postArray.push(socialItemObj)
        })
      
      this.postArray.sort((a,b) => {

          var dateA, dateB

          switch(a.source){
            case 'twitter':
              dateA = moment(a.published, 'ddd MMM DD HH:mm:ss ZZ YYYY')
            break;
            case 'youTube':
              dateA = moment(a.published)
            break;
            default:
              dateA = a.published
          }

          switch(b.source){
            case 'twitter':
              dateB = moment(b.published, 'ddd MMM DD HH:mm:ss ZZ YYYY')
            break;
            case 'youTube':
              dateB = moment(b.published)
            break;
            default:
              dateB = b.published
          }

          if(dateA < dateB){
            return -1;
          }

          if (dateA > dateB) {
            return 1;
          }

          return 0;
      })

      /*
      Benching this for now, this should be called to refresh the Bearer Token incase it has been invalidadted and the timeline called with the reurned token, This works in Postman 
      but I get a CORS preflight from the browser. I'm sure this is fixable but for the sake of time I'm moving on,
      and using a response obtained from postman and assigned to a js const in src/assets/twitterData.js.
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
  .social-list{
    width: 70%;
    margin-left: auto;
    margin-right: auto;
  }
</style>