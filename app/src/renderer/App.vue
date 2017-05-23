<template>
  <div id="app">
    <router-view></router-view>
  </div>
</template>

<script>
  import store from 'renderer/vuex/store'
  export default {
    store
  }
</script>

<style lang="stylus">
@import url(https://fonts.googleapis.com/css?family=Lato:300);

*
  margin: 0
  padding: 0

html, body, #app
  height: 100%
  user-select: none
  -webkit-app-region: drag

button
  -webkit-app-region: no-drag

body
  background: radial-gradient(
    ellipse at center,
    rgba(255, 255, 255, 1) 0%,
    rgba(229, 229, 229, .85) 100%
  )
  font-family: Lato, Helvetica, sans-serif
  text-align: center
</style>
