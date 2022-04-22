<template>
  <ul id="tv-item">
    <li>
      <img :src="img" :alt="title">
      <div class="d-none details">
        <span><strong>Titolo: </strong>{{title}}</span>
        <span><strong>Titolo originale: </strong>{{originalTitle}}</span>
        <span class="language"><strong>Lingua originale: </strong>{{originalLanguage}}</span>
        <span><strong>Voto: </strong></span>
        <span><strong>Overview: </strong>{{trama}}</span>
      </div>
    </li>
  </ul>

</template>
<script>
export default {
name: 'TvItemComp',
props : {
  img : String,
  title : String,
  originalTitle : String,
  originalLanguage : String,
  vote : Number,
  trama : String
},
methods : {
  
}
}
</script>

<style scoped lang='scss'>

#tv-item{
  width: calc(100% / 6);
  margin: 0.3em;
  background-color: #000;
  img{
    max-width: 100%;
    height: auto;
  }
  .details{
    color: #fff;
    margin: 1em 0.5em;
    overflow: hidden;
    text-overflow: ellipsis;
    span{
      margin: 0.2em;
    }
  }
}

#tv-item:hover img{
  display: none;
}

#tv-item:hover .details{
  display: unset;
  display: flex;
  flex-direction: column;
}
</style>