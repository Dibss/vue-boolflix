<template>
  <li class="flip-card">
    <div class="flip-card-inner">
      <div class="flip-card-front"
      :style="{backgroundImage : `url(https://www.themoviedb.org/t/p/w342/${tv.poster_path})`}"
      ></div>
      <div class="flip-card-back">
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
          <span v-for="i in 5" :key="i" :class="(i <= rated())? 'star' : ''"></span>
        </div>
        <div class="f-bold">Overview:
          <span>{{tv.overview}}</span>
        </div>
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
  rated(){
    const rounded = Math.ceil(this.tv.vote_average / 2);
    return rounded
  }
}
}
</script>

<style scoped lang='scss'>
.flip-card {
  background-color: transparent;
  width: 225px;
  height: 320px;
  perspective: 1000px;
}

.flip-card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}

.flip-card:hover .flip-card-inner {
  transform: rotateY(180deg);
}

.flip-card-front, .flip-card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
}

.flip-card-front {
  background-color: #bbb;
  color: black;
}

.flip-card-back {
  background-color: #000;
  color: white;
  transform: rotateY(180deg);
  padding: 1em;
  overflow-y: auto;
}

.star::before{content: "\2B50"; color: yellow;}

div.f-bold{margin-bottom: 0.5em;}

div > span{font-weight: normal;}

.flag-en::before{content: "	\01F1FA \01F1F8";}
.flag-it::before{content: '	\01F1EE \01F1F9';}
.flag-unknown::before{content : "\01F3F4 \200D \2620 \FE0F"}
</style>