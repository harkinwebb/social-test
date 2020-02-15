<template>
  <div class="card">
    <div class="card-thumb">
    </div>
    <div class="card-detail">
      <h3 class="post-title">{{cardData.title}}</h3>
      <div class="post-time">{{cardData.published}}</div>
      <div class="post-source">
        <font-awesome-icon :icon="['fab', 'youtube']" size="2x" class="youtube-icon" v-if="cardData.source == 'youTube'"></font-awesome-icon>
        <font-awesome-icon :icon="['fab', 'twitter']" size="2x" class="twitter-icon" v-else></font-awesome-icon>
      </div>
      <div class="post-body">{{cardData.description}}</div>
    </div>
  </div>
</template>

<script>
import {library} from '@fortawesome/fontawesome-svg-core'
import {faYoutube} from '@fortawesome/free-brands-svg-icons'
import {faTwitter} from '@fortawesome/free-brands-svg-icons'
import {FontAwesomeIcon} from '@fortawesome/vue-fontawesome'

library.add(faYoutube)
library.add(faTwitter)

export default {
  name: 'Card',
  components: {FontAwesomeIcon},
  props: {
    cardData: Object,
  }
}
</script>

<style scoped lang="scss">
  .card{
    margin-bottom: 20px;
  }

  .card-thumb{
    width: 20%;
    display:inline-block;
    border: 1px solid #373737;
    margin-right: 10px;
  }

  .card-detail{
    width: 78%;
    display:inline-block;
  }

  .twitter-icon{
    color: lightblue;
  }

  .youtube-icon{
    color: red;
  }

  .post-title{
    width:50%;
    display:inline-block;
    text-align: left;
    margin-bottom:10px;
  }

  .post-time{
    width:25%;
    display:inline-block;
    text-align: right;
    margin-bottom:10px;
  }

  .post-source{
    width:25%;
    display:inline-block;
    text-align: right;
    margin-bottom:10px;
  }

  .post-body{
    text-align: left;
  }
</style>