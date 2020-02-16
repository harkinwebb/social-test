<template>
  <div class="error-msg">
    {{errorMsg}}
  </div>
</template>

<script>

export default {
  name: 'ErrorMsg',
  props: {
    errorMsg: String,
  }
}
</script>

<style scoped lang="scss">
  .error-msg{
      padding: 20px;
      border-radius: 10px;
      border: 1px solid red;
      background-color: rgba(245, 0, 0, 0.24);
      margin-top: 20px;
      margin-bottom: 20px;
  } 
</style>