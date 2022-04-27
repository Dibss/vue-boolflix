<template>
  <li id="tv-item">
    <div class="img"
      :style="{backgroundImage : `url(https://www.themoviedb.org/t/p/w342/${tv.poster_path})`}"
    ></div>
    <div class="d-none details">
      <div class="f-bold">Titolo:
        <span>{{tv.title}}{{tv.name}}</span>
      </div>
      <div class="f-bold" v-show="tv.original_title && tv.original_name !== tv.title && tv.name">Titolo originale:
        <span>{{tv.original_title}}{{tv.original_name}}</span>
      </div>
      <div class="f-bold">Lingua originale:
        <span class="language" :class="(tv.original_language == 'en')? 'flag-en' : (tv.original_language == 'it')? 'flag-it': 'flag-unknown'"></span>
      </div>
      <div class="f-bold">Voto:
        <span>{{tv.vote_average}}</span>
      </div>
      <div class="f-bold">Overview:
        <span>{{tv.overview}}</span>
      </div>
    </div>
  </li>
</template>

<script>
export default {
name: 'TvItemComp',
props : {
  tv : Object
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
  height: 30%;
  overflow: hidden;
  .img{
    height: 30vh;
    width: 250px;
    background-position: center;
    background-size: cover;
    background-repeat: no-repeat;
  }
  .details{
    color: #fff;
    margin: 1em 0.5em;
    overflow: hidden;
    text-overflow: ellipsis;
    width: 250px;
    overflow-x: hidden;
    padding-right: 1em;
    span{
      margin: 0.2em;
    }
  }
}

div.f-bold{margin-bottom: 0.5em;}

div > span{font-weight: normal;}

.flag-en::before{content: "	\01F1FA \01F1F8";}
.flag-it::before{content: '	\01F1EE \01F1F9';}
.flag-unknown::before{content : "\01F3F4 \200D \2620 \FE0F"}

#tv-item:hover .img{
  display: none;
}

#tv-item:hover .details{
  display: unset;
  display: flex;
  flex-direction: column;
}
</style>