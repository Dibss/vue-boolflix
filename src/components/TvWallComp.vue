<template>
  <div id="tv-container">
    <TvItemComp/>
  </div>
</template>

<script>
import TvItemComp from "./partials/TvItemComp.vue"

export default {
name: 'TvWallComp',
components : {
  TvItemComp
}
}
</script>

<style scoped lang='scss'>
#tv-container{
  height: 92vh;
  background-color: #434343;
}
</style>