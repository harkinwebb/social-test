<template>
  <div class="card">
    {{cardData.title}}
    <br>
    {{cardData.description}}
    <br>
    {{cardData.published}}
    <br>
    {{cardData.source}}
    <br>
    <br>
  </div>
</template>

<script>
export default {
  name: 'Card',
  props: {
    cardData: Object,
  }
}
</script>

<style scoped lang="scss">

</style>