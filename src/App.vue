<template>
  <div id="app">
    <header>
      <HeaderComp/>
    </header>
    <main>
      <TvWallComp/>
    </main>
  </div>
</template>

<script>
import HeaderComp from "./components/HeaderComp.vue";
import TvWallComp from "./components/TvWallComp.vue"

export default {
  name: 'App',
  components: {
    HeaderComp,
    TvWallComp
  }
}
</script>

<style lang="scss">
*{padding: 0; margin: 0; box-sizing: border-box;}
#app {
  font-family: sans-serif;
}
</style>
