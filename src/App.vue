<template>
  <div id="app">
    <h1>Framestore social feed</h1>
    <router-view/>
  </div>
</template>

<style lang="scss">
$font-stack: Avenir, Helvetica, Arial, sans-serif;
$dark-text: #373737;
$standard-text: #626161; 

#app {
  font-family: $font-stack;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: $standard-text;
}

h1{
  color: $dark-text;
}

</style>
