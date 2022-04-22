<template>
  <div id="tv-container">
    <SearchComp @searchFunction="search"/>
    <!-- per le pagine : @pageSearch="searchPage" :pageArr="pageArr"  -->
    <div id="tv-wall" v-if="!loadingStatus">
      <TvItemComp v-for="film in filmArr" :key="film.id"
        :img="'https://www.themoviedb.org/t/p/w500/' + film.poster_path"
        :originalTitle="film.original_title"
        :title="film.title"
        :originalLanguage="film.original_language"
      />
      <TvItemComp v-for="serie in serieArr" :key="serie.id"
        :img="'https://www.themoviedb.org/t/p/w500/' + serie.poster_path"
        :originalTitle="serie.original_name"
        :title="serie.name"
        :originalLanguage="serie.original_language"
      />
      <ItemsFoundComp :items="filmArr.length + serieArr.length"/>
    </div>
    <div v-else id="loader">
      <LoaderComp/>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import TvItemComp from "./partials/TvItemComp.vue";
import SearchComp from "./partials/SearchComp.vue";
import ItemsFoundComp from "./partials/ItemsFoundComp.vue";
import LoaderComp from "./partials/LoaderComp.vue"

export default {
name: 'TvWallComp',
components : {
  TvItemComp,
  SearchComp,
  ItemsFoundComp,
  LoaderComp
},
data(){
  return{
    tvArr: [],
    filmArr : [],
    serieArr : [],
    page : 1,
    pageArr : [],
    loadingStatus: true,
  }
},
created(){
  this.get("a", 1);
  // this.getPage()
},
methods : {
  get(a, b){
    axios.get(`https://api.themoviedb.org/3/search/movie?api_key=1ddea58670cc4bdbfbe9d2d07181ce0c&query=${a}&page=${b}`)
      .then((res) => {
        console.log('FILM:', res.data.results);
        this.filmArr = res.data.results
      })
      .catch((error) => {
        console.log(error)
      });

    axios.get(`https://api.themoviedb.org/3/search/tv?api_key=1ddea58670cc4bdbfbe9d2d07181ce0c&page=${b}&query=${a}`)
      .then((res) => {
        console.log('SERIE:', res.data.results);
        this.serieArr = res.data.results
        this.loadingStatus = false;
      })
      .catch((error) => {
        console.log(error)
      })
  },
  // per le pagine
  // getPage(){
  //   axios.get(`https://api.themoviedb.org/3/search/movie?api_key=1ddea58670cc4bdbfbe9d2d07181ce0c&query=a`)
  //     .then((res) => {
  //       for(let i = 0; i < res.data.length; i++){
  //         if(this.pageArr.includes(res.data[i].page)){
  //           this.pageArr
  //         } else {
  //           this.pageArr.push(res.data[i].page)
  //         }
  //       }
  //       console.log("PAGES", this.pageArr)
  //     })
  //     .catch((error) => {
  //       console.log(error)
  //     })
  // },
  search( searchedText ){
    this.inputText = searchedText;
    console.log(this.inputText);
    this.get(this.inputText, this.page);
  },
  searchPage(page){
    this.selectedPage = page;
    console.log(this.selectedPage);
  },
  /*language : function(){
    switch( this.tvArr.original_language ){
      case "it":
        this.tvArr.original_language = "&#127470;"
        break;
      case "en":
        this.tvArr.original_language = "&#127482;"
        break;
    }
  }*/
}
}
</script>

<style scoped lang='scss'>
#tv-container{
  height: 100vh;
  background-color: #434343;
  overflow-y: auto;
  #tv-wall{
    display: flex;
    flex-wrap: wrap;
    width: 80%;
    margin: 2em auto;
  }
}
</style>