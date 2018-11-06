<template>
  <div id="app">
    <router-view/>
  </div>
</template>

<style lang="stylus">
html
  height 100%

body
  height 100%
  background linear-gradient(-20deg, #d0b782 20%, #a0cecf 80%)
  background-repeat no-repeat

#app
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
#nav
  padding 30px
  a
    font-weight bold
    color #2c3e50
    &.router-link-exact-active
      color #42b983
</style>
