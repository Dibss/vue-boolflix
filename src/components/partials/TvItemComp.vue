<template>
  <div id="tv-item">
    <img :src="img" :alt="title">
    <h2>{{title}}</h2>
    <span>{{originalTitle}}</span>
    <span class="d-block">{{originalLanguage}}</span>
  </div>
</template>

<script>
export default {
name: 'TvItemComp',
props : {
  img : String,
  title : String,
  originalTitle : String,
  originalLanguage : String,
  vote : Number
},
}
</script>

<style scoped lang='scss'>

#tv-item{
  width: calc(100% / 6);
  padding: 0.3em;
  img{
    max-width: 100%;
    height: auto;
  }
}
</style>