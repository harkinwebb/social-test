<template>
  <div class="card">
    <div class="card-thumb" v-if="cardData.image != ''">
      <img v-bind:src="cardData.image" />
    </div>
    <div class="card-thumb-spacer" v-else>
    </div>
    <div class="card-detail">
      <h3 class="post-title">{{cardData.title}}</h3>
      <div class="post-time">Posted {{cardData.postAge}} day/s ago</div>
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
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    justify-content: flex-start;
    align-items: flex-start;
  }

  .card-thumb{
    width: 20%;
    display:inline-block;
    margin-right: 10px;
    overflow: hidden;
    position: relative;
    height: 150px;
    border-radius: 20px;

    img{
      display: block;
      position: absolute;
      top: 50%;
      left: 50%;
      min-height: 100%;
      min-width: 100%;
      transform: translate(-50%, -50%);
    }
  }

  .card-thumb-spacer{
    width: 20%;
    display:inline-block;
    margin-right: 10px;
    overflow: hidden;
    position: relative;
  }

  .card-detail{
    width: 78%;
    display:inline-block;
    h3{
      margin-top: 0px;
    }
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