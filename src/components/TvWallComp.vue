<template>
  <div id="tv-container">
    <SearchComp @searchFunction="search" @pageSearch="selectPage" :pageArr="pageArr"/>
    <!-- per le pagine : @pageSearch="searchPage" :pageArr="pageArr"  -->
    <div id="tv-wall" v-if="!loadingStatus">
      <ul>
        <TvItemComp v-for="trending in trendingArr" :key="trending.id" v-show="!searchStatus"
          :tv="trending"
        />
        <TvItemComp v-for="film in filmArr" :key="film.id" v-show="searchStatus"
          :tv="film"
        />
        <TvItemComp v-for="serie in serieArr" :key="serie.id" v-show="searchStatus"
          :tv="serie"
        />
      </ul>
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
    trendingArr : [],
    filmArr : [],
    serieArr : [],
    page : 1,
    pageArr : [],
    loadingStatus: true,
    searchStatus : false,
  }
},
created(){
  this.get("a", this.page);
  this.pages();
  // this.getPage()
},
methods : {
  rated : function(){

  },
  // NON FUNZIONA
  doubleTitle : function(){
    this.filmArr.forEach(element => {
      if(element.title == element.original_title){
        this.filmArr.splice(element.original_title, 1)
      }
    });
  },
  get(a, b){
    axios.get(`https://api.themoviedb.org/3/trending/all/week?api_key=1ddea58670cc4bdbfbe9d2d07181ce0c`)
      .then((res) => {
        console.log('TRENDING:', res.data.results);
        this.trendingArr = res.data.results
      })
      .catch((error) => {
        console.log(error)
      });

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
    
    this.doubleTitle()
  },
  pages : function(){
    for(let i = 1; i < 1001; i++){
      this.pageArr.push(i);
    }
  },
  selectPage(page){
    this.page = page;
    console.log(this.page)
  },
  search( searchedText ){
    this.inputText = searchedText;
    console.log(this.inputText);
    this.searchStatus = true;
    this.get(this.inputText, this.page);
  },
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