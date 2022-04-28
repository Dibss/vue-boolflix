<template>
  <div id="app">
    <main>
      <TvWallComp/>
    </main>
  </div>
</template>

<script>
import TvWallComp from "./components/TvWallComp.vue"

export default {
  name: 'App',
  components: {
    TvWallComp
  }
}
</script>

<style lang="scss">
*{padding: 0; margin: 0; box-sizing: border-box;}
#app {
  font-family: sans-serif;
}

li{list-style-type: none; display: inline-block;}
.d-block{display: block;}
.d-none{display: none;}

.mb-2{margin-bottom: 1em;}
.my-2{margin-top: 1em; margin-bottom: 1em;}

.f-bold{font-weight: 700;}
</style>
